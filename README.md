# Advanced-SQL

Return the team names and the number of players in each team, all sorted by the number of players in each team, from the highest to the lowest.

SELECT t.name, count(*) as nb_of_player
FROM wizard w
inner JOIN player p ON w.id=p.wizard_id
inner JOIN team t ON t.id=p.team_id
GROUP BY t.name
order by nb_of_player desc;



Return the names of complete teams only (14 players or more, that is to say a minimum of 7 players and 7 substitute players), sorted by alphabetical order.

SELECT t.name, count(*) as nb_of_player
FROM wizard w
inner JOIN player p ON w.id=p.wizard_id
inner JOIN team t ON t.id=p.team_id
GROUP BY t.name
having nb_of_player >=14



Return a list of players in his team who were enrolled on a Monday (they want them to play first) and sort the results by enrollment date.

Select w.firstname, w.lastname, t.name, DATE_FORMAT(enrollment_date, "%a") as lucky_day, p.enrollment_date
from wizard w
inner JOIN player p ON w.id=p.wizard_id
inner JOIN team t ON t.id=p.team_id
where name = 'Gryffindor'  
order by case WHEN left(lucky_day, 1) = 'm' then 0 else 1 end
