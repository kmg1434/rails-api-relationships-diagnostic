# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

```sh
Say you wish to select... ugh i have a terrible imagination.
```

1.  Provide a database table structure and explain the Entity Relationship that
describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
(Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
`Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
join table with references to `Movies` and `Profiles`.

```sh
Im confused. You already explained the entity relationship between everything
for me, so Im not sure what to write.
```

1.  For the above example, what needs to be added to the Model files?

```rb
class Profile < ActiveRecord::Base
  has_many: movies, through: favorites
  has_many: favorites, dependent: destroy
end
```

```rb
class Movie < ActiveRecord::Base
  has_many: profiles, through: :favorites
  has_many: favorites, dependent: destroy
end
```

```rb
class Favorite < ActiveRecord::Base
  belongs_to :movie, inverse_of: :favorites
  belongs_to :profile, inverse_of: :favorites
end
```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

```sh
A serializer is thought of as a filter for database information. The serializer
 determines which columns will show when tables are viewed. Columns that are not
 shown do still exist however, they just wont be displayed.
```

```rb
class ProfileSerializer < ActiveModel::Serializer
  attributes :given_name, :surname, :email
end
```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

```sh
  bundl exec rails g scaffold favorites profile:string movie:string something:references
```

1.  What is `Dependent: Destroy` and where/why would we use it?

```sh
'Dependednt: Destroy' is used in a model when you wish to delete an item that is
dependent on another item. Imagine a movie is deleted from the database; you
would also have to delete this movie from user favorites
```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

```sh
A forum board user only has 1 avatar/signature, but that avatar/signature could
be the same as another user. "an avatar has_many users". A user has many
favorites (favorite posts or forum catagories), and a favorite has many users.
```
