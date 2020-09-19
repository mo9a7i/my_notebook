```javascript


adonis make:migration members            --Rename later
adonis make:migration posts
adonis make:migration categories
adonis make:migration config
adonis make:migration comments
adonis make:migration reports            -- Maybe split, for comments and posts
adonis make:migration likes
adonis make:migration pages

adonis make:model Post -mc
adonis make:model Category -mc
adonis make:model Comment -mc
adonis make:model Page -mc
```

