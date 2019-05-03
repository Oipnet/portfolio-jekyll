---
layout: blog_entry
image: /img/banner.jpg
title: Enregistrer un model sans déclencher d'évènements
category: laravel
banner: true
---

Au moment de l'enregistrement en base de données laravel déclenche des évènement grace au mécanisme d'[Observers](https://laravel.com/docs/5.8/eloquent#observers). 
Il est parfoit nécessaire de désactiver ce mecanisme. 
<!--more-->

Dans un tweet Taylor Otwell nous délivre une solution pour ne pas les déclencher
``` php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    public function saveQuietly(array $options= [])
    {
        return static::withoutEvents(function () use ($options) {
            return $this->save($options);
        });
    }
}

```
Source : [Twitter @taylorotwell](https://twitter.com/taylorotwell/status/1123239506994499584?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1123239506994499584&ref_url=https%3A%2F%2Fmurze.be%2Fexecute-eloquent-methods-without-firing-events)
