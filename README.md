# MySQL Query Project

Bài tập lớn cuối kì môn cơ sở dữ liệu 

## Authors

* **Lê Ngọc Anh Quân** - *20176852* - [Link github](https://github.com/quan191)

* **Nguyễn Vũ Long** - *20176809* - [Link github](https://github.com/LongNguyenVu181)



## Đề bài 

Xây dựng cơ sở dữ liệu và viết các câu truy vấn với database đó 

## Phần mềm sử dụng và database sử dụng 

* MySQL - The web framework used
* MySQL WorkBench - Sử dụng để tạo ER diagram và các câu truy vấn
* Premiere League (https://relational.fit.cvut.cz/dataset/PremiereLeague) - Database sử dụng 

## List các câu hỏi 

* 1 In ra tổng số bản thắng của từng đội trong mùa giải.
```
SELECT B.name , SUM(A.goals) as GoalsInSeason
FROM actions as A
JOIN teams as B 
ON A.teamID=B.teamID
GROUP BY A.teamID;
```

* 2 In ra vua phá lưới của mùa giải 2011-2012
```
SELECT A.name, sum(B.goals) as GoalsInSeason
 FROM players as A 
JOIN actions as B 
ON A.PlayerID=B.PlayerID 
JOIN matches as C 
ON B.matchID=C.matchID 
WHERE year(C.date) IN (2011,2012)
 GROUP BY A.PlayerID 
ORDER BY GoalsInSeason DESC LIMIT 1;
```

* 3 Lấy ra kết quả và số bàn thắng của các trận 2 đội Manchester United và Arsenal gặp nhau trong cả mùa giải
```
SELECT A.MatchID , Date,
(SELECT name FROM teams where teamID=A.TeamHomeID) as TEAMHOME,
 (SELECT name FROM teams where teamID=A.TeamAwayID) as TEAMAWAY ,
 concat(sum(if(B.teamID=A.TeamHomeID,goals,0)),'-', 
 sum(if(B.TeamID=A.TeamAwayID,goals,0))) as Score 
 FROM matches as A 
JOIN actions as B 
ON	A.matchID=B.matchID 
WHERE  A.TeamHomeID IN 
(SELECT teamID 
from teams 
WHERE  name IN ('Arsenal','Manchester United')) 
AND A.TeamAwayID IN 
(SELECT teamID 
FROM teams
 WHERE
  name IN ('Manchester United','Arsenal')) 
group by A.matchID;  
```





