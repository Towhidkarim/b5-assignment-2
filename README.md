# 📘 PostgreSQL প্রশ্নোত্তর

## ১। What is PostgreSQL?

PostgreSQL হল একটি ওপেন সোর্স ডেটাবেস, বর্তমান যুগ এর সব থেকে জনপ্রিয় ডেটাবেস সিস্টেম গুলোর একটি । PG বা PSQL হিশেবেও অনেক জায়গায় পরিচিত। এটি একটি রিলেশনাল ডেটাবেস যেটি tabular format বা row এবং column আকারে ডেটা স্টোর করে। ডেটা এক্সেস করার জন্য SQL ল্যাঙ্গুয়েজ ব্যাবহার করা হয় । PostgreSQL এ মডার্ন ডেটাবেস এর প্রায় সকল ফিচার রয়েছে এবং ইন্ডাস্ট্রি তে বহুল ব্যাবহার করা হয়ে থাকে । রোবাস্ট স্কেলইং এবং ইন্ডাস্ট্রি স্ট্যান্ডার্ড এর জন্য PostgreSQL একটি উত্তম চইস

---

## ২। Explain the Primary Key and Foreign Key concepts in PostgreSQL.

**Primary Key** একটি constraint, যেটা টেবিল এর কোন (সুধু ) একটি কলাম এর উপর apply করা হয়, এবং এইটা বুঝায় যে ঐ কলাম এর মাধ্যমে ওই row টা কে ইউনিকলি identify করা যাবে। এটা একটা ইউনিক column বা column এর value , এবং এইটা null হতে পারে না। Primary Key ব্যাবহার করা হয় ইউনিক column গুলো খুঁজে বের করতে এবং তাদের উপর কোন অপারেশন চালাতে। এইগুলা অন্য table এ foreign key হিসেবেও use করা যায়, যাতে করে অন্য কোন relation কে reference দেয়া যায়। এটা define করা হয় PRIMARY KEY clause এর মাধ্যমে। যেমন একটি ছাত্রের primary key হতে পারে তার রোল নম্বর।

**Foreign Key** একটা constraint, যেটা যে কোন সংখ্যক কলাম এর উপর apply করা যেতে পারে, যেখানে ঐ কলাম এর value আরেকটা table এর primary key এর value হয়ে থাকে, মানে সেটা আরেকটা table এর সাথে সম্পর্ক স্থাপন করে। এটা apply করা যায় FOREIGN KEY ক্লজ ব্যাবহার করে, অথবা column define করার সময়ই REFERENCES clause দিয়ে সরাসরি করা যায়। যেমন , যদি কোন course teacher এর table এ department_id নামে একটা কলাম থাকে, ওটা foreign key হিসেবে department টেবিল কে রেফার করতে পারে।

---

## ৩। What is the difference between the VARCHAR and CHAR data types?

**CHAR** আর **VARCHAR** দুটাই string data type, কিন্তু ডেটা স্টোর করার ক্ষেত্রে ওদের মধ্যে কিছু পার্থক্য রয়েছে ।  
**CHAR** হলো একটা fixed length data type। মানে, যদি আমরা CHAR(50) ডিফাইন করি, তাহলে এটা 50 characters এর জন্য জায়গা রিজার্ভ করে নিবে, না কম, না বেশি, একেবারে fixed।

কিন্তু **VARCHAR** এর ক্ষেত্রে, এটা used space অনুযায়ী storage allocate করে। ধরা যাক , যদি VARCHAR(50) ব্যবহার করি, তাহলে সর্বোচ্চ ৫০ character পর্যন্ত ডেটা স্টোর করতে পারা যাবে । কিন্তু যদি ইনপুট ডেটা ৫০ character এর কম হয়, তাহলে এটা শুধুমাত্র ওই ডেটার সাইজ অনুযায়ী জায়গা নিবে, পুরো ৫০ character জায়গা নষ্ট করবে না। তবে, এই ক্ষেত্রে ৫০ character এর বেশি স্টোর বা গ্রহন করবে না।

---

## ৪। Explain the purpose of the WHERE clause in a SELECT statement.

যখন SELECT clause ব্যাবহার করে কোন কিছু column select করা হয় বা column এর ডাটা নেওয়া হয়, তখন WHERE clause ব্যাবহার করে সেই selection টার অপর বিভিন্ন condition অ্যাপ্লাই করা যায় ।  
WHERE এর পরে যেকোনো condition দিয়ে দিলে সেটা মেইন্টেইন করে selection টা সম্পন্ন হয় এবং ডাটা ডিসপ্লে করা হয়।

এক কথায় বলতে গেলে SELECT statement এ WHERE clause ব্যাবহার করে selection আরও properly specify করা হয় বা আরও specific selection করা হয় use-case এর অপর নির্ভর করে।

---

## ৫। What are the LIMIT and OFFSET clauses used for?

LIMIT clause টি ব্যাবহার করা হয় ডেটাবেস থেকে কতটি row শো করা হবে তা নির্ধারণ করতে। এবং , OFFSET ব্যাবহার করা হয় কতটি রো স্কিপ করে তারপর থেকে রেজাল্ট দেখাবে তা নির্ধারণ করতে।  
এগুলো সাধারণত **pagination** এর ক্ষেত্রে ব্যাবহার করা হয়।

যেমন যদি কথার কথা দ্বিতীয় পেজ এ ১০টি ডেটা থাকে , সেই ক্ষেত্রে, পার পেজ যেহেতু ১০টা, তাই:

```sql
LIMIT 10 OFFSET 10
```

(LIMIT data_per_page OFFSET  
data_per_page \* page_number - 1) এই ক্রাইটেরিয়া অনুযায়ী pagination সম্পন্ন হবে ।
