- 160 API requests per minute for ENTIRE app (not one instance!) (changed to 30+ req/s but it costs quite a lot
- limited number of COUNT operations (differs every time, but surely under 160)
- if you are counting objects with the count higher that just a 1000, the system switches to “approximate count”
- any function can not take longer than 3 seconds
- if that function is in a cloud that time can last 7 seconds
- scheduled jobs can last a maximum of 15 minutes, but you have to put ALL of your code in one function (which basically makes it unreadable for later usages)
- maximum of 2 concurrent jobs (threads)
- no mutex/lock/semaphore logic
- no custom atomic operations (just a few are available, and they are not that useful)
this makes it very very hard to solve concurrency problems
- log system remembers only 100 last logs
- live logging in the system has a tendency to simply skip a log or two (which makes debugging really funny)
- you can pull a maximum of 1000 objects in a request, which also applies on inner queries
push notifications have delay (even up to one hour)
- LIMIT SKIP operation can skip a maximum of 10 000 objects
- no DISTINCT operation, you have to implement distinct yourself by parsing data
- lack of incase sensitive string queries, you need to store additional lowercase column in your database
- uptime of parse system is also an issues. Quite a few times, parse was unavailable in general for 30minutes
- no native Paypal integration support, or ability to implement paypals SDK – we had to use separate node.js hosting server to support payments and cash distribution through Paypay
- no debugger when writing cloudcode – you have to rely on logs only, and they have their own issues mentioned above