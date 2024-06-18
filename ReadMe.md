CREATE DATABASE MMORPG;
USE MMORPG;
```
description TEXT,

CREATE TABLE account (
```
account_id INT PRIMARY KEY AUTO_INCREMENT,
account_name VARCHAR(50) UNIQUE NOT NULL,
FOREIGN KEY (character_id) REFERENCES character(character_id)
monthly_fee DECIMAL(10, 2) NOT NULL,

CREATE TABLE character (
BEGIN
character_id INT PRIMARY KEY AUTO_INCREMENT,
character_name VARCHAR(50) NOT NULL,
team VARCHAR(50),
skill_level INT,
account_id INT,
FOREIGN KEY (account_id) REFERENCES account(account_id)
);
```
CREATE TABLE item (
item_id INT PRIMARY KEY AUTO_INCREMENT,
item_name VARCHAR(50) NOT NULL,
quantity INT NOT NULL,
INSERT INTO item (item_name, quantity, character_id) VALUES (item_name, qty, char_id);

CREATE TABLE error (
error_id INT PRIMARY KEY AUTO_INCREMENT,
error_type VARCHAR(50) NOT NULL,
```
account_id INT,
FOREIGN KEY (account_id) REFERENCES account(account_id)
CREATE VIEW vwTopStackedItems AS
);
INSERT INTO account (account_name, monthly_fee, status) VALUES
('player1', 15. 99, 'unblocked'),

```sql
('player2', 15. 99, 'blocked');

INSERT INTO character (character_name, team, skill_level, account_id) VALUES
('char1', 'teamA', 10, 1),
('char2', 'teamB', 20, 2);
```
INSERT INTO item (item_name, quantity, character_id) VALUES
('sword', 2, 1),
CREATE VIEW vwBlockedAccounts AS
('shield', 1, 2);
```
INSERT INTO error (error_type, description, account_id) VALUES
('login_error', 'Failed login attempt', 1),
('payment_error', 'Payment declined', 2);

status ENUM('blocked', 'unblocked') NOT NULL
);

```sql
```
```sql
SELECT * FROM account WHERE status = 'blocked';

CREATE VIEW vwTopSkill AS
SELECT * FROM character ORDER BY skill_level DESC LIMIT 20;
```

SELECT item_name, SUM(quantity) AS total_quantity
FROM item
GROUP BY item_name
ORDER BY total_quantity DESC LIMIT 20;
```

CREATE VIEW vwPopItems AS
SELECT item_name, COUNT(character_id) AS num_characters
GROUP BY item_name
ORDER BY num_characters DESC LIMIT 5;
```
CREATE PROCEDURE spRegister(IN acc_name VARCHAR(50), IN fee DECIMAL(10, 2), IN stat ENUM('blocked', 'unblocked'))
BEGIN
IF NOT EXISTS (SELECT * FROM account WHERE account_name = acc_name) THEN
INSERT INTO account (account_name, monthly_fee, status) VALUES (acc_name, fee, stat);
END IF;
END;
```

```sql
CREATE PROCEDURE spAddTime(IN acc_name VARCHAR(50), IN days INT)
BEGIN
IF EXISTS (SELECT * FROM account WHERE account_name = acc_name) THEN
UPDATE account SET status = 'unblocked' WHERE account_name = acc_name;
END IF;
END;
```
CREATE PROCEDURE spAddItem(IN char_id INT, IN item_name VARCHAR(50), IN qty INT)
END IF;
END;
```
CREATE PROCEDURE spAddChar(IN char_name VARCHAR(50), IN team VARCHAR(50), IN skill INT, IN acc_id INT)
BEGIN
INSERT INTO character (character_name, team, skill_level, account_id) VALUES (char_name, team, skill, acc_id);
END;
```

CREATE PROCEDURE spSendLetter(IN acc_name VARCHAR(50), IN news TEXT)
BEGIN
SELECT CONCAT('Dear ', acc_name, ', you have ', (SELECT status FROM account WHERE account_name = acc_name), ' days left. ', news) AS letter;
END;
```

CREATE TRIGGER after_account_insert
AFTER INSERT ON account
FOR EACH ROW
BEGIN
INSERT INTO error (error_type, description, account_id) VALUES ('info', 'New account created', NEW. account_id);
END;
```
CREATE TRIGGER after_character_insert
AFTER INSERT ON character
FOR EACH ROW
BEGIN
INSERT INTO error (error_type, description, account_id) VALUES ('info', 'New character created', NEW. account_id);
END;
```
CREATE INDEX idx_account_name ON account(account_name);
CREATE INDEX idx_character_name ON character(character_name);
CREATE INDEX idx_item_name ON item(item_name);
```

