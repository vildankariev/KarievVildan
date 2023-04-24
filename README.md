# KarievVildan
use vk;
 
select (select concat(u.firstname, ' ', u.lastname) from users u where u.id = p.user_id) as 'Name',
  if(p.gender = 'f', 'Женщина', 'Мужчина') as 'Gender',
  date_format(p.birthday, '%d %M %Y') as 'DOB'
from profiles p
order by 1;

select u.firstname as 'Name', coalesce(u.email, u.phone, 'Не задан') as 'Contacts' from users u;

select substring_index(u.email, '@', -1) as 'Email' from users u group by substring_index(u.email, '@', -1);

select (select concat(u.firstname, ' ', u.lastname) from users u where u.id = p.user_id), ((year(curdate()) - year(p.birthday)) - (date_format(p.birthday, '%m%d') > date_format(curdate(), '%m%d'))) as 'Age', if(datediff(curdate(), p.birthday) < 6574, 'Несовершеннолетний', 'Совершеннолетний') as 'status' from profiles p;

select substring_index(m.filename, '.', 1) as 'Filename', round(m.size, -4) as 'Size' from media m;

select m.filename, replace(m.created_at, created_at, curdate()) as 'rewritten date' from media m where m.user_id in (select u.id from users u where u.firstname = 'Frederic' and u.lastname = 'Upton');

select monthname(p.birthday) as 'Name', count(p.user_id) as 'Count' from profiles p group by monthname(p.birthday);
