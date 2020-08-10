# Security

## How to create a SQL injection attack with Shift-JIS and CP932?
http://stackoverflow.com/questions/28705324/how-to-create-a-sql-injection-attack-with-shift-jis-and-cp932
http://stackoverflow.com/questions/5741187/sql-injection-that-gets-around-mysql-real-escape-string/12118602#12118602

### Test char: \ x5c
http://www.isthisthingon.org/unicode/index.phtml?glyph=bf5c
http://www.rtpro.yamaha.co.jp/RT/docs/misc/kanji-sjis.html

## Solution
http://stackoverflow.com/questions/10113562/pdo-mysql-use-pdoattr-emulate-prepares-or-not

```
$pdo->setAttribute(PDO::ATTR_EMULATE_PREPARES, false);
```
