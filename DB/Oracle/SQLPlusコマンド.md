# SQL\*Plus コマンド

## SQL\*Plus の接続書式

```
# OS認証を使用して接続
sqlplus / as sysdba

# Usernameのみ指定
sqlplus username@tnsname

# Password も指定
sqlplus username/password@tnsname

# sysdba で接続
sqlplus sys/password@tnsname as sysdba

# 簡易接続ネーミング・メソッド
sqlplus username/password@//host:port/servicename
```

## ユーザーの作成

PDB に接続して実行

書式

```
CREATE USER <ユーザ名> IDENTIFIED BY <パスワード>
```

実行例

```
SQL> CREATE USER non IDENTIFIED BY N0n_Passw0rd;

User created.

SQL>
```

## ユーザーに権限付与

例

```
GRANT CONNECT, RESOURCE TO non;
```

実行例

```
SQL> GRANT CONNECT, RESOURCE TO non;

Grant succeeded.

SQL>
```

作成したユーザーで接続

```
sqlplus non/N0n_Passw0rd@pdbname
```

## ユーザーを指定して、表領域 Quota の上限を無制限に変更

```
ALTER USER <username> quota unlimited on <table space name>;
```

実行例

```
SQL> ALTER USER non quota unlimited on USERS;

User altered.

SQL>
```

## ユーザーに紐づく PROFILE のパスワード有効期限を無効にする

```
ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;
```

## ユーザー一覧

```
select username from dba_users;
```

## テーブル一覧

DBA 権限の場合

```
select owner,table_name from dba_tables;
```

ログインしているユーザーが参照できるすべてのテーブルを表示

```
select owner,table_name from all_tables;
```

ログインしているユーザーが OWNER のテーブルを表示

```
select table_name from USER_TABLES;
```
