\# Bug 07 — API нь буруу/байхгүй нөөцөд амжилттай (2xx) гэж хариулдаг



\*\*Severity:\*\* Medium

\*\*Олдсон аялал:\*\* Saboteur — Байхгүй id, буруу JSON, хоосон body илгээж API-ийн алдааны хариуг туршсан.

\*\*Орчин:\*\* Opera 137.0.6036.63, Node.js v24.22.1, http://localhost:3000



\## Урьдчилсан нөхцөл (Preconditions)

Апп ажиллаж байгаа.



\## Reproduce хийх алхмууд

1\. `curl.exe -i -X DELETE http://localhost:3000/api/books/999`

2\. `curl.exe -i -X POST http://localhost:3000/api/books -H "Content-Type: application/json" -d '{buruu'`

3\. `curl.exe -i -X POST http://localhost:3000/api/books` (body-гүй)

4\. `curl.exe -i -X DELETE http://localhost:3000/api/books/5` хоёр удаа дараалан



\## Хүлээгдэж буй үр дүн (Expected)

\- Байхгүй номыг устгахад 404

\- Буруу JSON-д 400

\- Хоосон body-д 400 (validation алдаа)



\## Бодит үр дүн (Actual)

\- DELETE байхгүй id → HTTP 200 OK `{"result":"OK"}`

\- Буруу JSON → HTTP 200 OK `{"result":"OK"}` (ном үүсээгүй)

\- Body-гүй POST → HTTP 201 Created `{"result":"OK","id":4}`, хоосон ном үүссэн

\- Устсан номыг дахин устгахад мөн 200 OK



\## Нотолгоо (Evidence)

\- `evidence/` дотор хадгалсан curl гаралтууд (доор тайлбарласан)



\## Нэмэлт тэмдэглэл

Клиент хүсэлт амжилтгүй болсныг статус кодоор мэдэх боломжгүй.



