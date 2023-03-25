# Creating Entity.php

The entity file **without** foreign relationships.

```php
<?php

namespace Modules\Blog\Entities;

use Modules\Base\Entities\BaseModel;
use Illuminate\Database\Schema\Blueprint;

class Content extends BaseModel
{

    protected $fillable = ['title', 'slug'];
    protected $table = "blog_content";

    /**
     * List of fields for managing postings.
     *
     * @param Blueprint $table
     * @return void
     */
    public function migration(Blueprint $table)
    {

        $table->increments('id');
        $table->string('title')->nullable();
        $table->string('slug')->nullable();
    }
}

```

The entity **with** foreign relationships.

```php
<?php

namespace Modules\Blog\Entities;

use Modules\Base\Entities\BaseModel;
use Illuminate\Database\Schema\Blueprint;

class Content extends BaseModel
{

    protected $fillable = ['title', 'slug'];
    public $migrationDependancy = ['blog_category']; // Table name that has foreign fields in this table.
    protected $table = "blog_content";
    
    /**
     * List of fields for managing postings.
     *
     * @param Blueprint $table
     * @return void
     */
    public function migration(Blueprint $table)
    {

        $table->increments('id');
        $table->string('title')->nullable();
        $table->string('slug')->nullable();
        $table->integer('category_id')->nullable();
    }
    
    
   public function post_migration(Blueprint $table)
    {
        if (Migration::checkKeyExist('blog_content', 'category_id')) {
            $table->foreign('category_id')->references('id')->on('blog_category')->nullOnDelete();
        }
    }
}

```
