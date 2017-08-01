
UNIVERSAL - EJS
===
universal react
===============
1. performance
reduce the amount of http request needed to render the initial html and data
2. SEO compliant
universal apps can be indexed by search engines


npm i --save-dev ejs


BACKUP DB
=========
mongodump --db bookshop --out .

UPLOAD DB TO MLAB
=================
mongorestore -h ds129053.mlab.com:29053 -d minus-plus-bookshop -u minus-plus -p mimanicai .

CREDENTIAL
==========
minus-plus: miminicai

CONNECTION
==========
mongoose.connect('mongodb://minus-plus:mimanicai@ds129053.mlab.com:29053/minus-plus-bookshop');
