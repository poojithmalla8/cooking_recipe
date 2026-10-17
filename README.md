# 🍳 My Recipe Collection

A personal cookbook built from my Instagram **"Cooking"** saved collection — every recipe I've saved, organized in one cozy place with ingredients, step-by-step cooking method, average cooking time, calories, the perfect moment to cook it, and a food classification (Breakfast, Entree, Main Course, Side Dish, Snack, Dessert, Beverage).

🌐 **Browse the cookbook:** https://poojithmalla8.github.io/cooking_recipe  
*(enable GitHub Pages on `main` branch if the link doesn't open yet: Settings → Pages → Deploy from branch → main)*

## What's inside

| File | Description |
|---|---|
| `index.html` | The recipe webpage — search, category/cuisine filters, sorting, and a detail view per recipe |
| `data/recipes-*.json` | The recipe database, sharded JSON (loaded by the page) |

## Recipe record schema

```jsonc
{
  "id": "chicken-leg-ghee-curry",   // url-safe slug
  "name": "Chicken Leg Ghee Curry",
  "category": "Main Course",        // Breakfast | Entree | Main Course | Side Dish | Snack | Dessert | Beverage
  "cuisine": "Indian",              // guessed from the dish name / TheMealDB, null if unknown
  "ingredients": [{"item": "chicken", "measure": "500 g"}],
  "steps": ["Marinate the chicken...", "..."],   // how to cook, in order
  "time_min": 40,                   // average cooking time in minutes
  "time_source": "estimated",       // "from post" when a creator stated it, else "estimated"
  "calories": 600,                  // per serving
  "calories_source": "estimated",   // "from post" when a creator stated it, else "estimated"
  "best_time_to_cook": "Relaxed weekend cooking & family dinners",
  "image": "https://...",           // dish photo (TheMealDB), null if none
  "youtube": "https://...",         // video recipe (TheMealDB), null if none
  "recipe_source": "themealdb",     // "themealdb" | "caption" | "estimated"
  "saved_count": 2                   // how many saved posts mapped to this dish
}
```

## How the database was built

1. **Pulled** all posts from the Instagram "Cooking" saved collection (889 posts).
2. **Extracted** dish names from captions; parsed `Ingredients:` / `Method:` sections, stated calories and cooking times where creators included them.
3. **Matched** dishes against [TheMealDB](https://www.themealdb.com) (790 meals) for full ingredient lists, step-by-step methods, photos, and video links.
4. **Classified** each dish (Breakfast / Entree / Main Course / Side Dish / Snack / Dessert / Beverage) and **estimated** missing cooking times & calories per category — always labeled `"estimated"` so you know what's a rough guide vs. stated by the creator.

Caveats: dish names come from free-form captions, so a few may be slightly off; estimated times/calories are guides, not measurements. When in doubt, check the linked video recipe.
