# Mission 3

## Part 1,2 

[Link to folder](https://drive.google.com/drive/folders/1cUfD8jWtsl6yxNlOV80eIaVta48Thqib?usp=sharing)

## Part 3

- Запрос 1 Получить список юзернеймов пользователей\
SELECT username\
FROM users;

- Запрос 2 Получить кол-во отправленных сообщений каждым пользователем\
SELECT u.username, COUNT(m.id) AS total_messages\
FROM users u\
JOIN messages m ON u.id = m.from\
GROUP BY u.username;

- Запрос 3 Пользователя с самым большим кол-вом полученных сообщений и само количество\
ELECT u.username, COUNT(m.id) AS total_messages\
FROM users u\
JOIN messages m ON u.id = m.from\
GROUP BY u.username\
HAVING COUNT(m.id) = (\
SELECT COUNT(m2.id) AS max_messages\
FROM messages m2\
GROUP BY m2.from\
ORDER BY max_messages DESC\
LIMIT 1\
);

- Запрос 4 Получить среднее кол-во сообщений, отправленное каждым пользователем\
SELECT u.username, AVG(sent_messages.count) AS average_sent_messages\
FROM (\
SELECT from AS user_id, COUNT(*) AS count\
FROM messages\
GROUP BY from\
) sent_messages\
JOIN users u ON u.id = sent_messages.user_id\
GROUP BY u.username;
  
