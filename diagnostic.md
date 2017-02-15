# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

  ```md
    If we take instance of a recipe app which has both recipe and ingredients table. Each time that we are creating a new recipe an instance of ingredients will be used several times as a result of this we will need to
    create new raws for those instances. However if we have joint tables we won't need this repetitievness.
  ```

1.  Provide a database table structure and explain the Entity Relationship that
  describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
  (Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
  `Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
  join table with references to `Movies` and `Profiles`.

  ```md
    Profiles has many movies through favorites
    Movies has many profiles through faorites
  ```

1.  For the above example, what needs to be added to the Model files?

  ```rb
  class Profile < ActiveRecord::Base
  has_many :movies through: :favorites
  has_many :favorites
  end
  ```

  ```rb
  class Movie < ActiveRecord::Base
  has_many :profiles through: :favorites
  has_many :favorites
  end
  ```

  ```rb
  class Favorite < ActiveRecord::Base
  belongs_to :movie
  belongs_to :profile
  end
  ```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

  ```md
  Serializer will be controlling and shaping the data we are sending to database.
  ```

  ```rb
  class ProfileSerializer < ActiveModel::Serializer
  attributes :given_name :surname :email

  def favorites
  object.favorites.pluck(:id)
  end
  end
  ```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

  ```sh
    bin/rails generate scaffold favorirtes date_on:date date_of:date 
  ```

1.  What is `Dependent: Destroy` and where/why would we use it?

  ```md
    If we have ralationship between our tables, for instance atuhors wit many
    books and if we would like the books to be deleted when we delete the author then we use Dependent: Destroy`. When the objext is destroy associated objects will be destroyed.
  ```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

  ```md
    One actor will be having many movies in cds.
    Many cds will be any borrowers and there will be a joint table for as loans
  ```
