classDiagram

%% =====================
%% Base Entity (optional but clean design)
%% =====================

class BaseEntity {
  <<abstract>>
  +UUID id
  +DateTime created_at
  +DateTime updated_at
  +save()
  +update()
  +delete()
}

%% =====================
%% Core Entities
%% =====================

class User {
  +String first_name
  +String last_name
  +String email
  +String password
  +Boolean is_admin
  +register()
  +update_profile()
}

class Place {
  +String title
  +String description
  +Float price
  +Float latitude
  +Float longitude
  +add_amenity()
  +remove_amenity()
  +update_details()
}

class Review {
  +Integer rating
  +String comment
  +update_review()
}

class Amenity {
  +String name
  +String description
  +update_amenity()
}

%% =====================
%% Inheritance
%% =====================

User --|> BaseEntity
Place --|> BaseEntity
Review --|> BaseEntity
Amenity --|> BaseEntity

%% =====================
%% Relationships
%% =====================

User "1" --> "0..*" Place : owns
User "1" --> "0..*" Review : writes

Place "1" *-- "0..*" Review : contains

Place "0..*" --> "0..*" Amenity : has