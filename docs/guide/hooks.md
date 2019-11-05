# Hooks

One of the powerful features of Laravel Orion is Hooks. It allows you to tap into a flow inside a particular (or multiple) endpoints without the need to override a method itself.

Here is a common use case: imagine you have an API controller for blog posts and whenever a blog post is created, it needs to be associated with the currently authenticated user. To accomplish that, simply add `beforeSave` hook and attach user to the post:

```php
<?php

namespace App\Http\Controllers\API;

use App\Models\Post;
use Laralord\Orion\Http\Requests\Request;
use Laralord\Orion\Http\Controllers\Controller;

class PostsController extends Controller
{
    /**
     * @var string|null $model
     */
    protected static $model = Post::class;

    /**
     * @param Request $request
     * @param Post $post
     */
    protected function beforeSave(Request $request, $post)
    {
        $post->user()->associate($request->user());
    }
}
```

## On model controllers

* beforeIndex - executed before retrieving the list of models.
* afterIndex - executed after retrieveing the list of models, but before building response.
* beforeShow - executed before retrieving a model.
* afterShow - executed after retrieving a model, but before building response.
* beforeStore - executed before creating a new model instance and filling out attributes.
* afterStore - executed after storing a model, but before building response.
* beforeUpdate - executed before retrieving a model and filling out attributes.
* afterUpdate - executed after updating a model, but before building response.
* beforeSave - executed before model is saved, but after `beforeStore` and `beforeUpdate`.
* afterSave - executed after model is saved, but before `afterStore` and `afterUpdate`.
* beforeDestroy - executed before retrieving a model and deleting it.
* afterDestroy - executed after deleting a model, but before building response.
* beforeRestore - executed before retrieving a model and restoring it.
* afterRestore - executed after restoring a model, but before building response.

## On relationship controllers

**All types:** same as model controllers, relation controllers have before and after hooks for CRUD operations.

**One to many:**

* beforeAssociate - executed after retrieving both models, but before associating a child model.
* afterAssociate - executed after saving a relation model with associated child model id, but before building response.
* beforeDissociate - executed after retrieving both models, but before dissociating a child model.
* afterDissociate - executed after saving a relation model with associated child model id, but before building response.

**Many to many:**

* beforeSync - executed before retrieving a relation model.
* afterSync - executed after syncing related models, but before building response.
* beforeToggle - executed before retrieving a relation model.
* afterToggle - executed after toggling related models, but before building response.
* beforeAttach - executed before retrieving a relation model.
* afterAttach - executed after attaching related model(s) to a relation model, but before building response.
* beforeDetach - executed before retrieving a relation model.
* afterDetach - executed after detaching related model(s) from a relation model, but before building response.
* beforeUpdatePivot - executed before retrieving a relation model.
* afterUpdatePivot - executed after updating pivot of related model, but before building response.