# SQL-Bisnis
Project SQL tentang Bisnis

#Kita akan memberikan promosi untuk customer perempuan di kota Depok melalui email. Tolong berikan data ada berapa customer yang harus diberikan promosi per masing-masing jenis email
SELECT
  id,
  email
FROM
  `belajar-sql-366206.ecommerce.customer`
WHERE
  gender = 'Female'
  AND city= 'Depok'
  
#10 id customer dengan total pembelian overall terbesar untuk diberikan diskon campaign 9.9
 SELECT
  customer_id,
  SUM(total) AS total_pembelanjaan
FROM
  `belajar-sql-366206.ecommerce.transaction`
GROUP BY
  1
ORDER BY
  2 DESC
LIMIT
  10
  
#Produk di database yang mempunyai harga kurang dari 10000
SELECT  
id AS product_id
FROM `belajar-sql-366206.ecommerce.product` 
WHERE price<10000

#list 5 produk yang paling banyak dibeli
SELECT 
product_id,
SUM(quantity) AS total_terjual
 FROM `belajar-sql-366206.ecommerce.transaction`
 GROUP BY 1
 ORDER BY 2 DESC
 LIMIT 5

#Jumlah transaksi, pendapatan dan jumlah produk yang terjual di platform secara bulanan. Apakah terjadi kenaikan atau penurunan?
SELECT
  DATE_TRUNC(created_at, MONTH),
  COUNT(DISTINCT id) AS count_transaction,
  SUM(total) AS total_pendapatan,
  SUM(quantity) AS total_terjual
FROM
  `belajar-sql-366206.ecommerce.transaction`
GROUP BY
  1
ORDER BY
  1 ASC
  
#Total belanja dan rata-rata belanja customer per kota
SELECT 
a.city,
SUM(b.total) AS total_pembelanjaan,
AVG(b.total) AS avg_pembelanjaan
 FROM `belajar-sql-366206.ecommerce.transaction` b 
 LEFT JOIN
 belajar-sql-366206.ecommerce.customer a 
 ON a.id=b.customer_id
 GROUP BY 1
 
#Jumlah customer yang memiliki total belanja keseluruhan lebih dari 200000 berdasarkan tipe storenya
SELECT 
type,
COUNT (DISTINCT customer_id) jumlah_customer
 FROM `belajar-sql-366206.ecommerce.transaction` a
 LEFT JOIN
 belajar-sql-366206.ecommerce.store b
ON
a.store_id=b.id
GROUP BY 1
HAVING
SUM(total)>200000
ORDER BY 2
DESC
