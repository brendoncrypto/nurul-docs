# Prompt Favorites Feature

The Favorites feature allows users to save prompts they find useful for quick access later. This document outlines how the feature works, its implementation details, and how to use it.

## User Flow

1. **Favoriting Prompts**:
   - Users can favorite prompts from the Prompt Library by clicking the star icon on any prompt card
   - Favorited prompts are saved to the user's account and persist across sessions

2. **Viewing Favorites**:
   - Favorited prompts can be accessed from:
     - Dashboard → Favorites link in the sidebar
     - The dedicated Favorites page at `/dashboard/favorites`
     - A preview of favorites is shown on the dashboard home

3. **Managing Favorites**:
   - Users can remove prompts from favorites by clicking the star icon again
   - The Favorites page provides pagination for browsing through all saved prompts

## Technical Implementation

### Database Schema

The favorite functionality relies on two main tables:

1. **`prompts`**: Stores the actual prompt data
   - Contains fields like `prompt_text`, `primary_concern`, `therapeutic_theme`, etc.
   - Has counters for `likes` and `views`

2. **`user_favorites`**: Junction table connecting users to their favorited prompts
   - Contains `user_id`, `prompt_id`, and `created_at` fields
   - Has a unique constraint on the combination of `user_id` and `prompt_id`

### API Endpoints

The following API endpoints handle favorite-related operations:

1. **GET `/api/user/favorites`**
   - Retrieves a user's favorited prompts
   - Supports pagination with `page` and `limit` parameters
   - Returns prompt data along with pagination information

2. **POST `/api/user/favorites`**
   - Adds a prompt to the user's favorites
   - Requires a `promptId` in the request body
   - Checks for existing favorites to prevent duplicates

3. **DELETE `/api/user/favorites?promptId=123`**
   - Removes a prompt from the user's favorites
   - Requires the `promptId` as a query parameter

### Component Integration

1. **`PromptCard`** Component:
   - Displays a star icon that indicates favorite status
   - Handles toggling favorite status via API calls
   - Updates UI immediately for a responsive feel
   - Checks favorite status on component mount

2. **`FavoritesPage`** Component:
   - Displays a grid of favorited prompts
   - Supports pagination for browsing through favorites
   - Shows appropriate messaging when no favorites exist
   - Includes filtering and sorting options

## Security Considerations

- All favorite operations require authentication
- Row-level security policies ensure users can only:
  - View their own favorites
  - Add prompts to their own favorites list
  - Remove prompts from their own favorites list

## Future Enhancements

1. **Favorite Collections**: Allow users to organize favorites into collections
2. **Favorite Sharing**: Enable sharing favorite lists with other users
3. **Bulk Operations**: Add ability to favorite/unfavorite multiple prompts at once
4. **Smart Recommendations**: Suggest similar prompts based on favorites

## Troubleshooting

If favorites are not displaying correctly:

1. Ensure the user is properly authenticated
2. Check browser console for API errors
3. Verify database tables and RLS policies are correctly set up
4. Clear browser cache if experiencing stale data issues 