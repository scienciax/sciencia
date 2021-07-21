---
layout: post
title:  "SQL Injections"
author: adeesha
categories: [Computer Security]
tags: [ Computer Science,Database Security, SQL Injections ]
image: "https://raw.githubusercontent.com/scienciax/sciencia/master/assets/images/posts/ajp/cov/sqli.png"

---

SQL Injection කියන්නෙ වෙබ් ආරක්ෂාව ගැන කතා කරනකොට මග හරින්නම බැරි මාතෘකාවක්. ඒ වගේම SQL Injection වලට ස්ථිරසාර විසඳුමක් දෙන එකත් කරන්න අපහසුම වැඩක්. SQL Injection ගැන හොයන්න කලින් අපිට සිද්ධ වෙනව Relational Database සහ SQL එහෙමත් නැත්තං Structured Query Language කියන්නෙ මොනවද කියල කෙටියෙන් දැනගන්න.



#### Relational Database

දත්ත ගබඩා කරන්නත් එකිනෙකට සම්බන්ධතා තියන, ගබඩා කරපු දත්ත වලට ප්‍රවේශය දෙන්නත් පුළුවන් විදිහට සැලසුම් කරපු ඩේටා බේස් වර්ගයක් තමයි Relational Database කියන්නෙ. මේ ඩේටාබේස් වල දත්ත ගබඩා කරන්නෙ වගු (table) වල. මේ වගුවක තීරු (Column) වලින් ඒ දත්ත වල උපලක්ෂණ එහෙමත් නැත්තං ගුණ (attributes) දක්වනව. එකඋපලක්ෂණයකට එක කොලම්එකක් බැගින් තියෙන්න ඕනි. හැම ටේබල් එකකටම එම දත්තයට විතරක් අනන්‍ය (unique) වෙච්ච ගුණයක් තියන කොලම් එකක් තියෙන්න ඕනි. මේ කොලම් එක ඒ ටේබල් එකේ කී (key) එක හැටියට සලකනව. (primary key etc..) මේ කී එක වෙන ටේබල් වල තියන කොලම් එකකට සමාන නං, ඒ හරහා ටේබල් අතර සම්බන්ධතාවය හදන්න පුළුවන්. මෙන්න මේ හේතුව නිසා මේ ඩේටාබේස් වර්ගයට Relational Database කියල කියන්නෙ.



#### Structured Query Language

Relational Database වලින් වැඩ ගන්නම නිර්මාණය කරපු භාෂාවක්. මේක domain-specific language එකක්. ඒ කියන්නෙ විශේෂ කාර්යක් විතරක් කරන්න නිර්මාණය කරපු භාෂාවක්. HTML, MATLAB කියන්නෙත් මේ ජාතියේ භාෂා දෙකක්. SQL පාවිච්චි කරල බොහොම ලේසියෙන් රිලේෂනල් ඩේටාබේස් පරිපාලනය කරන්න පුළුවන්. විවිධ ටේබල් ගණනාවක තියන දත්ත අවශ්‍ය හැටියට අරගෙන තාවකාලිකව තනි ටේබල් එකක් නිර්මාණය කරගන්න. ඒ දත්ත විවිධ කටයුතු වලට පාවිච්චි කරන්න වගේම නැවත දත්ත ලියන්නත් මේ හරහා පුළුවන්. අදාළ දත්ත ඇත්තටම ස්ටෝරේජ් මීඩියා වල තියෙන්නේ කොහෙද, කොහොමද දත්ත ටේබල් වලින් ගන්නෙ වගේ කරුණු ගැන කරදර නොවී සරල query එකකින් අවශ්‍ය දත්ත ලබාගන්න පුළුවන්.

![SQL Flow](https://raw.githubusercontent.com/scienciax/sciencia/master/assets/images/posts/ajp/cont/sqli1.JPG?raw=true)

--------

**Relational නොවෙන database වර්ගයකුත් තියනව. NoSQL ඩේටාබේස් කියන නමිනුත් හඳුන්වන්නෙ ඒ වර්ගයම තමයි. ඒව නිර්මාණය කරලා තියෙන්නෙ relational නොවෙන ආකාරයට දත්ත ගබඩා කරන්න. relational database වලින් කරගන්න බැරි සමහර දේවල් මේ relational නොවෙන database වලින් කරගන්න පුළුවන්. විශාල දත්ත ප්‍රමාණයක් කළමනාකරණය කරනකොට relational database වල කාර්යක්‍ෂමතාව බොහොම අඩු වෙනව. මේ NoSQL ඩේටාබේස් ඉතාම පහසුවෙන් විශාල ප්‍රමාණ වලට Scale කරන්න, කොටස් වශයෙන් පාවිච්චි කරන්න වගේම සමහර දත්ත පරිශීලකයාගේ පැත්තෙ තියල භාවිතා කරන්නත් පුළුවන්.**

--------



#### SQL Injections

මොකක්ද මේ SQL Injections කියන්නෙ. මෙතනදී කරන්නෙ උඩ අපි උදාහරණෙ පෙන්නපු query එක වගේ එකක් රන් කරද්දී ඊට අමතරව වෙන query එකකුත් ඒත් එක්කම රන් කරන එක, වෙබ් ඇප්ලිකේෂන් එකෙන් පරිශීලකයාට ඉඩ දෙන query ඇරෙන්න වෙන query රන් කරවන එක වගේ වැඩ වලට. මෙතනදී SQL වල තියන සමහර පහසුකම් වැරදි විදිහට භාවිතා කිරීමක් සිද්ධ වෙනව. මෙතන තියන ලොකුම ප්‍රශ්නෙ මේ පහසුකම් නීත්‍යානුකුල වැඩ වලටත් අවශ්‍ය වෙන නිසා ඉවත් කරන්න බැරි එක. ඒ කියන්නෙ ඉතින් SQL පාවිච්චි වෙනකල් SQL Injections කියන ප්‍රශ්නයත් තියනව කියන එක තමයි.

පරිශීලකයාගෙන් විවිධ දත්ත අරගෙන ඒ දත්ත ඇසුරෙන් ඩේටාබේස් එක සම්බන්ධ විවිධ වැඩ කරන වෙබ් අඩවි වලට,වෙබ් ඇප් වලට, මෘදුකාංග වලට මේ වර්ගයේ ප්‍රහාර එල්ල වෙන්න පුළුවන්.

ඉහත උදාහරණය ටිකක් විස්තරාත්මකව බලමු.

**මේ ඒ වැඩේට හරියන සරල වෙබ් ෆෝම් එකක්**

<hr>


<form>
  <label for="district">Province:</label><br>
  <input type="text" id="district" name="district"><br><br>
  <button disabled>Search Districts</button>
</form> 



<hr>

**මේ ඒ ෆෝම් එකට අදාළ php කෝඩ් එක.**

<hr>

// ඩේටාබේස් එක එක්ක කනෙක්ෂන් එක හදනව

$conn = mysql_connect("localhost","username","password");

// පරිශීලකයා දෙන දත්ත අනුව query එක හදනව

$query = "SELECT * FROM districts WHERE province = '$_GET["district"]';

// query එක රන් කරනව

$result = mysql_query($query);

// query එකෙන් එක ප්‍රථිපල පිළිවෙලකට සකසනව

while($row = mysql_fetch_array($result, MYSQL_ASSOC))

{

// display the results to the browser

echo "District: {$row['NameDistrict']}".

"Province : {$row['Province']}".

"Population : {$row['Populatn']} ";

}



<hr>

දැන් අපි උඩ තියන උදාහරණය එක්කම පොඩ්ඩක් පැහැදිලි කරන්න බලමු SQL Injection එකක් වැඩ කරන හැටි.


උඩ තියන query එක වෙන්නෙ SELECT * FROM districts WHERE province = 'south' කියන එක. අපි මේක පහසු වෙන්න කොටස් වලට කඩාගමු

SELECT *  - මෙතනින් කියන්නෙ පහත ප්‍රකාශය සත්‍ය වෙන, දත්ත වලට අදාළ කොලම් ඔක්කොම තෝරන්න කියල.

FROM districts - මේ තියෙන්නෙ පහත ප්‍රකාශයට සම්බන්ධ ටේබල් එක.

WHERE province = 'south' - මෙන්න ප්‍රකාශය.

SQL වල ප්‍රකාශ එකකට වඩා දෙන්න පුළුවන්. උදාහරණයක් හැටියට province = 'south' එක්ක OR province = 'west' කියල දෙන්නත් පුළුවන්.

ඒ කියන්නෙ WHERE province = 'south' OR province = 'west' කියල.

දැන් කෙනෙක්ට ඔය පහසුකම වැරදි විදිහට පාවිච්චි කරන්න පුළුවන්.

SELECT * FROM districts WHERE province = 'south' OR 'zoo' = 'zoo' කියන query එක බලන්න. මෙතන දැන් ප්‍රකාශ දෙකක් තියනව. එකක් province = 'south' අනිත් එක 'zoo' = 'zoo'. දැන් අපි බලමු database එක කොහොමද මේ query එක රන් කරන්නෙ කියල.

![SQL Injection flow](https://raw.githubusercontent.com/scienciax/sciencia/master/assets/images/posts/ajp/cont/sqli2.JPG?raw=true)

මෙතන තියන භයානක කම තමයි අර අන්තිම ප්‍රකාශය වෙනුවට ටේබල් එකක් සම්පුර්ණයෙන් මකන්න, ටේබල් වල දත්ත මකන්න, වෙනස් කරන්න, Login Credentials ලබාගන්න වගේම ඩේටාබේස් සර්වර් එකට යම් බලපෑම් කරන්න අවශ්‍ය වෙන කමාන්ඩ් උනත් දෙන්න පුළුවන් වීම.

එකවර SQL quarries එකකට වඩා රන් කරන්න ඉඩ දෙන ඩේටාබේස් සර්වර් වල Batched SQL Statements රන් කරල හානිදායක ක්‍රියා සිද්ධ කරන්නත් පුළුවන්.

උදාහරණයක් හැටියට SELECT * FROM districts WHERE province = 'south'; DROP TABLE users;

කියන විධාන දෙකම එකවර ";" මගින් වෙන් කරල දෙන්න පුළුවන්. ඒ හරහා users කියන ටේබල් එක මකන්න පුළුවන්.



#### SQL Injections ප්‍රහාර වර්ග

**Unsanitized Input** - පරිශීලකයාගෙන් එන දත්ත හරියට "පිරිසිදු" නොකර පාවිච්චි කරනව නං මේ වගේ ප්‍රහාර වලට ලක්වෙන්න හොඳටම ඉඩ තියනව. sanitize කරනව කියන එකෙන් කරන්නෙ පරිශීලකයාගෙන් එන දත්ත අපි බලාපොරොත්තු වෙන විදිහට තියනවද කියල තහවරු කරලා, එහෙම නැති දත්ත නොසලකා හරින එක හරි පරිශීලකයා එවන දත්ත වල අනවශ්‍ය characters තියනව නං එවුව අයින් කරන එක. !, $, %, * වගේ characters තියනව නං අනිවාර්යයෙන් එවුව අයින් කරන්න ඕනි. php වල තියන real_escape_string වගේ උපක්‍රම වලින් මේ වැඩේ කරන්න පුළුවන්.

**Blind SQL Injection** - මෙතනදී කරන්නෙ True or False වර්ගයේ queries විතරක් පාවිච්චි කරල ඒ queries වලට එන ප්‍රතිචාරය අනුව ඩේටාබේස් එකේ තොරතුරු දැනගන්න එක. මේ ක්‍රමය පාවිච්චි වෙන්නෙ වැරදි queries වලට ඩේටාබේස් එකෙන් දෙන error message වෙනුවට generic error messages පෙන්නන විදිහට ආරක්‍ෂිත උපක්‍රම පාවිච්චි කරන අවස්ථා වල. ඒ වගේම Time-based Blind SQL injection වලදී queries වලින් ප්‍රථිපල එන එක යම් කාලයක් ප්‍රමාද කරනව. මේ ප්‍රමාද වෙන කාලය ඇසුරෙන් True or False තත්වය තීරණය කරනව.

**Out-of-Band Injection** - කෙලින්ම query වලට ප්‍රතිචාර ගන්න බැරි අවස්ථා වලදී විශේෂ queries පාවිච්චි කරල ඩේටාබේස් සර්වර් එක ප්‍රහාරකයා විසින් පාලනය කරන සර්වර් එකකට සම්බන්ධ වෙන්න සලස්වල අවශ්‍ය තොරතුරු ගන්න එක. මේක තරමක් සංකීර්ණ ක්‍රමයක් ලු.



#### SQL Injections වලින් බේරෙන හැටි

**No dynamic SQL** - පරිශීලකයන් ගෙන් ගන්න දත්ත කෙලින්ම පාවිච්චි කරන්න එපා. ඒ වගේම පුළුවන් තරම් parameterized queries පාවිච්චි කරන්න.

**No sensitive data in plaintext** - password වගේ දත්ත කිසිම වෙලාවක ඒ විදිහටම ඩේටාබේස් එකක ඇතුලත් කරන්න හොඳම නෑ. හොඳ hashing ක්‍රමයක් පාවිච්චි කරන්නම ඕනි. එතකොට මොනයම් ක්‍රමයකින් හරි password එක ගත්තත් එතන තියෙන්නෙ "$2y$10$0Lsw25KnfrsjtQKepe1eq.3WVO8TkKA.sIqh433deWD511t9N9hd." වගේ අගයක්.

**Sanitize user inputs** - පරිශීලකයන් එවන දත්ත නිසි පරිදි පරීක්ෂා කරන්න ඕනි. ඔවුන් එවන දත්ත වර්ගය අපි බලාපොරොත්තු වෙන දත්ත වර්ගයද කියන එක, ඒ දත්ත ඇතුලෙ escape characters තියද බලල එවුව අයින් කරන එක අනිවාර්යයෙන් කරන්න ඕනි.

**Limit database permissions and privileges** - ඩේටාබේස් එකක වැඩිම බලතල තියෙන්නෙ root account එකට. උඩ php කෝඩ් එකේ තිබ්බ $conn = mysql_connect("localhost","username","password"); කියන කොටසේ තියෙන්නෙ වෙබ් අඩවියට එන ඉල්ලීම් ඩේටාබේස් එකත් එක්ක සම්බන්ධ කරන user account එක. මේ user account එකට තියන බලතල පුළුවන්තරම් අඩු කරොත් (අවශ්‍ය ප්‍රමාණයට විතරක්) හානිදායක SQL quarries රන් වෙන එක නවත්තන්න පුළුවන්. උදාහරණයක් හැටියට දත්ත ඇතුලත් කිරීමක් වෙන්නෙ නැත්තං read-only විතරක් පුළුවන් user account එකක් පාවිච්චි කරන එක වැදගත්.

**Avoid displaying database errors** - මෙන්න මේ error message වලින් අපේ ඩේටාබේස් එකට අදාළ විවිධ තොරතුරු ගන්න පුළුවන්. ඒ තොරතුරු පාවිච්චි කරල විවිධ quarries රන් කරල අවශ්‍ය තොරතුරු ලබාගන්න පුළුවන්. ඒ නිසා error message වලින් තොරතුරු එලි නොවෙන විදිහට custom error message ඉදිරිපත් කරන්න ඕනි.

**Use a Web Application Firewall** - SQL Injections කරන්න හදන අවස්ථා අඳුනගන්න පුළුවන්. එහෙම අවස්ථා වලින් එක හානිකර SQL queries නවත්තන්න පුළුවන්.

**Up-to-date Database**  - ඩේටාබේස් සර්වර් හරියට යාවත්කාලීන කරලා තියන්න අවශ්‍යයි. එතකොට ඩේටාබේස් සර්වර් එකේ තියන දුර්වලතා හරහා එන ප්‍රහාර වලින් වැළකෙන්න පුළුවන්.



**මේ ලිපියෙන් ඉදිරිපත් කරේ SQL Injection ගැන පොඩි විස්තරයක්.**



**Reference**

[Relational Databases Explained -  IBM](https://www.ibm.com/cloud/learn/relational-databases)

[What is a Relational Database](https://www.oracle.com/database/what-is-a-relational-database/)

[NoSQL Databases - IBM](https://www.ibm.com/cloud/learn/nosql-databases)

[Out-of-band SQL - Acunetix](https://www.acunetix.com/blog/articles/sqli-part-6-out-of-band-sqli/)

[Blind SQL Injection -  OWASP](https://owasp.org/www-community/attacks/Blind_SQL_Injection)

[SQL Injection Prevention - OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html#Defense_Option_1:_Prepared_Statements_.28with_Parameterized_Queries.29)

[What is SQL Injection? Attack Examples & Prevention - Rapid7](https://www.rapid7.com/fundamentals/sql-injection-attacks/)

Clarke, J. (2009) “What Is SQL Injection?,” in *SQL Injection Attacks and Defense*. Elsevier, pp. 1–27.

Morgan, D. (2006) “Web application security – SQL injection attacks,” *Network security*, 2006(4), pp. 4–5.

Cherry, D. (2015) “SQL Injection Attacks,” in *Securing SQL Server*. Elsevier, pp. 265–291.



**Image Credits**

[Cover Image - avast](https://www.avast.com)
