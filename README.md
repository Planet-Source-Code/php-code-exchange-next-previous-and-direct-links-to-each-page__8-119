<div align="center">

## Next, Previous, and direct links to each page \#


</div>

### Description

This is the code that I use to get xxx entries per page from a database. It also provides direct page links (i.e. if there are 3 pages of db entries, you will see Prev 1 2 3 Next). by Matt Whitted
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[PHP Code Exchange](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/php-code-exchange.md)
**Level**          |Intermediate
**User Rating**    |5.0 (15 globes from 3 users)
**Compatibility**  |PHP 3\.0, PHP 4\.0
**Category**       |[Databases](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/databases__8-5.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/php-code-exchange-next-previous-and-direct-links-to-each-page__8-119/archive/master.zip)





### Source Code

```
<? php
// Simple chunk of code to take a db query and display it xx entries
// per page, by Matt Whitted (admin@virtuaweb.net).
// Not the cleanest code, but it works.
// Number of entries per page
$per_page = 25;
// You will need to change this. This should be your normal SQL query that
// you use to get the info to be displayed from the db.
$sql_text = ("SELECT * from table");
// Set page #, if no page isspecified, assume page 1
if (!$page) {
  $page = 1;
}
$prev_page = $page - 1;
$next_page = $page + 1;
$query = mysql_query($sql_text);
// Set up specified page
$page_start = ($per_page * $page) - $per_page;
$num_rows = mysql_num_rows($query);
if ($num_rows <= $per_page) {
  $num_pages = 1;
} else if (($num_rows % $per_page) == 0) {
  $num_pages = ($num_rows / $per_page);
} else {
  $num_pages = ($num_rows / $per_page) + 1;
}
$num_pages = (int) $num_pages;
if (($page > $num_pages) || ($page < 0)) {
  error("You have specified an invalid page number");
}
//
// Now the pages are set right, we can
// perform the actual displaying...
$sql_text = $sql_text . " LIMIT $page_start, $per_page";
$query = mysql_query($sql_text);
while ($result = mysql_fetch_array($query)) {
  // This stuff is obviously just an example. This is where you want
  // to layout your HTML to display the queries. This loop will run
  // once for every entry to be displayed on the current page.
  echo $result[email];
  echo "<br>";
}
// You will probably want to modify this stuff too. This displays
// the previous, next, and direct links to each page. It is laid out
// VERY plain below, so you will likely want to change it to fit the
// layour of your site.
// Previous
if ($prev_page) {
  echo "<a href=\"$PHP_SELF page=$prev_page\">Prev</a>
}
// Page # direct links
// If you don't want direct links to each page, you should be able to
// safely remove this chunk.
for ($i = 1; $i <= $num_pages; $i++) {
  if ($i != $page) {
   echo " <a href=\"$PHP_SELF?page=$i\">$i</a> ";
  } else {
   echo " $i ";
  }
}
// Next
if ($page != $num_pages) {
  echo "<a href=\"$PHP_SELF page=$next_page\">Next</a>
}
?>
```

