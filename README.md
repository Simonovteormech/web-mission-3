# web-mission-3
# VIDEO
Link to video

# SQL

-- Получить список юзернеймов пользователей
SELECT username FROM users;

-- Получить кол-во отправленных сообщений каждым пользователем
SELECT username, COUNT(*) AS "number of sent messages" 
FROM messages 
JOIN users ON messages.from = users.id 
GROUP BY username;

-- Получить пользователя с самым большим кол-вом полученных сообщений и само количество
SELECT username, COUNT(*) AS "number of received messages" 
FROM messages 
JOIN users ON messages.to = users.id 
GROUP BY username 
ORDER BY COUNT(*) DESC 
LIMIT 1;

-- Получить среднее кол-во сообщений, отправленное каждым пользователем
SELECT username, AVG(cnt) AS "average number of sent messages" 
FROM (
    SELECT messages.from, COUNT(*) AS cnt 
    FROM messages 
    GROUP BY messages.from
) AS message_count 
JOIN users ON message_count.from = users.id 
GROUP BY username;
