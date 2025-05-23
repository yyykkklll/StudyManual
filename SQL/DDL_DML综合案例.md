# DDL_DML综合案例

---

### 案例目标：设计一个图书管理系统
系统需要管理图书、借阅者和借阅记录，能够：
- 存储图书信息（书名、作者、价格等）
- 记录借阅者信息（姓名、联系方式等）
- 跟踪借阅记录（谁借了哪本书、何时借还）
- 支持查询和统计功能

---

### 第一步：数据库设计（DDL）
我们需要创建以下表：
1. `books`：图书表
2. `borrowers`：借阅者表
3. `borrow_records`：借阅记录表

#### 1. 创建数据库
```sql
CREATE DATABASE library_system;
USE library_system;
```

#### 2. 创建图书表（books）
```sql
CREATE TABLE books (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100) NOT NULL,
    author VARCHAR(50) NOT NULL,
    price DECIMAL(6,2),
    stock INT DEFAULT 0,
    INDEX idx_title (title) -- 为常用查询字段添加索引
);
```

#### 3. 创建借阅者表（borrowers）
```sql
CREATE TABLE borrowers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    phone VARCHAR(20),
    UNIQUE INDEX idx_phone (phone) -- 电话号码唯一
);
```

#### 4. 创建借阅记录表（borrow_records）
```sql
CREATE TABLE borrow_records (
    id INT PRIMARY KEY AUTO_INCREMENT,
    book_id INT,
    borrower_id INT,
    borrow_date DATE,
    return_date DATE,
    FOREIGN KEY (book_id) REFERENCES books(id),
    FOREIGN KEY (borrower_id) REFERENCES borrowers(id)
);
```

#### 5. 添加触发器
自动更新图书库存：借出时减少库存，还书时增加库存。
```sql
DELIMITER //
CREATE TRIGGER after_borrow_insert
AFTER INSERT ON borrow_records
FOR EACH ROW
BEGIN
    UPDATE books SET stock = stock - 1 WHERE id = NEW.book_id;
END //

CREATE TRIGGER after_return_update
AFTER UPDATE ON borrow_records
FOR EACH ROW
BEGIN
    IF NEW.return_date IS NOT NULL AND OLD.return_date IS NULL THEN
        UPDATE books SET stock = stock + 1 WHERE id = NEW.book_id;
    END IF;
END //
DELIMITER ;
```

---

### 第二步：初始数据插入（DML）
#### 1. 插入图书
```sql
INSERT INTO books (title, author, price, stock) VALUES
('西游记', '吴承恩', 50.00, 5),
('红楼梦', '曹雪芹', 60.50, 3),
('水浒传', '施耐庵', 45.00, 4);
```

#### 2. 插入借阅者
```sql
INSERT INTO borrowers (name, phone) VALUES
('张三', '13812345678'),
('李四', '13987654321'),
('王五', '13755556666');
```

#### 3. 插入借阅记录
```sql
INSERT INTO borrow_records (book_id, borrower_id, borrow_date, return_date) VALUES
(1, 1, '2025-03-01', NULL), -- 张三借了西游记
(2, 2, '2025-03-02', '2025-03-10'); -- 李四借了红楼梦并归还
```

当前数据：
- `books`：
```
id | title    | author  | price | stock
1  | 西游记   | 吴承恩 | 50.00 | 4
2  | 红楼梦   | 曹雪芹 | 60.50 | 3
3  | 水浒传   | 施耐庵 | 45.00 | 4
```
- `borrowers`：
```
id | name  | phone
1  | 张三  | 13812345678
2  | 李四  | 13987654321
3  | 王五  | 13755556666
```
- `borrow_records`：
```
id | book_id | borrower_id | borrow_date | return_date
1  | 1       | 1           | 2025-03-01  | NULL
2  | 2       | 2           | 2025-03-02  | 2025-03-10
```

---

### 第三步：数据操作与查询（DML）
#### 1. 查询所有未归还的借阅记录
```sql
SELECT b.title, br.name, r.borrow_date
FROM borrow_records r
INNER JOIN books b ON r.book_id = b.id
INNER JOIN borrowers br ON r.borrower_id = br.id
WHERE r.return_date IS NULL;
```
结果：
```
title   | name  | borrow_date
西游记  | 张三  | 2025-03-01
```

#### 2. 更新归还日期
张三归还《西游记》：
```sql
BEGIN;
UPDATE borrow_records SET return_date = '2025-03-19' WHERE id = 1;
COMMIT;
```
触发器自动更新库存，`books` 表：
```
id | title    | author  | price | stock
1  | 西游记   | 吴承恩 | 50.00 | 5
...
```

#### 3. 统计每本书的借阅次数
```sql
SELECT b.title, COUNT(r.id) AS borrow_count
FROM books b
LEFT JOIN borrow_records r ON b.id = r.book_id
GROUP BY b.id, b.title
HAVING borrow_count > 0;
```
结果：
```
title   | borrow_count
西游记  | 1
红楼梦  | 1
```

#### 4. 查询库存不足的图书
```sql
SELECT title, stock
FROM books
WHERE stock < 2;
```
当前无结果（库存都大于2）。

#### 5. 用窗口函数排名借阅者
假设增加更多借阅记录：
```sql
INSERT INTO borrow_records (book_id, borrower_id, borrow_date) VALUES
(3, 3, '2025-03-05'), -- 王五借水浒传
(1, 2, '2025-03-15'); -- 李四再借西游记
```

按借阅次数排名：
```sql
SELECT br.name, COUNT(r.id) AS borrow_count,
       RANK() OVER (ORDER BY COUNT(r.id) DESC) AS borrow_rank
FROM borrowers br
LEFT JOIN borrow_records r ON br.id = r.borrower_id
GROUP BY br.id, br.name;
```
结果：
```
name  | borrow_count | borrow_rank
李四  | 2            | 1
张三  | 1            | 2
王五  | 1            | 2
```

---

### 小练习
请根据当前系统完成以下任务：
1. 用 DDL 创建一个 `categories` 表（图书分类，包含 `id` 和 `name`），并将 `books` 表与它关联。
2. 用 DML 插入两条分类数据（如“小说”和“历史”），并更新 `books` 表添加分类。
3. 写一个查询，显示每个分类的图书总数和平均价格。
4. 开始一个事务，将王五的借阅记录（book_id = 3）的归还日期设为今天（2025-03-19），并提交。

---

