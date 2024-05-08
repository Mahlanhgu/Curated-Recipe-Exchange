@startuml

class User {
    - id: int
    - username: String
    - email: String
    - password: String
    + login(username: String, password: String): boolean
    + logout(): void
    + register(username: String, email: String, password: String): boolean
    + resetPassword(email: String): boolean
    + createRecipe(title: String, description: String, ingredients: String[], instructions: String): void
    + editRecipe(recipe: Recipe, newTitle: String, newDescription: String, newIngredients: String[], newInstructions: String): void
    + deleteRecipe(recipe: Recipe): void
}

class Recipe {
    - id: int
    - title: String
    - description: String
    - ingredients: String[]
    - instructions: String
    - author: User
    + rate(stars: int): void
    + review(comment: String): void
    + addToCollection(collection: RecipeCollection): void
    + removeFromCollection(collection: RecipeCollection): void
}

class RecipeCollection {
    - id: int
    - name: String
    - recipes: List<Recipe>
    + addRecipe(recipe: Recipe): void
    + removeRecipe(recipe: Recipe): void
    + getRecipes(): List<Recipe>
    + getRecipeById(id: int): Recipe
}

class UserInterface {
    - currentUser: User
    + displayLoginScreen(): void
    + displayRegisterScreen(): void
    + displayHomeScreen(): void
    + displayRecipeDetails(recipe: Recipe): void
    + displayUserProfile(user: User): void
    + displayRecipeCollection(collection: RecipeCollection): void
    + displayEditRecipeScreen(recipe: Recipe): void
    + displayDeleteConfirmation(recipe: Recipe): void
}

class Database {
    - users: Map<Integer, User>
    - recipes: Map<Integer, Recipe>
    - recipeCollections: Map<Integer, RecipeCollection>
    + saveUser(user: User): void
    + saveRecipe(recipe: Recipe): void
    + saveRecipeCollection(collection: RecipeCollection): void
    + getUser(id: int): User
    + getRecipe(id: int): Recipe
    + getRecipeCollection(id: int): RecipeCollection
    + getAllRecipes(): List<Recipe>
}

User "1" --> "*" Recipe : writes
Recipe "1" --> "0..1" RecipeCollection : belongs to
UserInterface "1" --> "1" User : uses
UserInterface "1" --> "1" Database : interacts with

@enduml
