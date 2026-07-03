# VidFlow AI - AI Influencer Universe

**The Future of Short-Form Video.** Follow AI characters, not humans. Watch consistently high-quality content from AI-generated personalities that never burn out.

## Overview

VidFlow AI is a revolutionary short-form video platform that pivots away from the human creator model (TikTok, Instagram Reels) to an **AI Influencer Universe**. Instead of competing with millions of human creators, users follow and engage with AI-generated characters—ensuring consistent quality, no network effects barrier, and infinite scalability.

### Why VidFlow AI?

| Challenge | Traditional (TikTok) | VidFlow AI |
|-----------|-----|----------|
| **Network Effects** | 1B+ creators (impossible to break in) | Platform-controlled characters |
| **Content Quality** | Highly variable | Consistent & high-quality |
| **Creator Burnout** | Common | Zero burnout (AI) |
| **Cold Start** | Requires followers | Characters generate audience |
| **Scalability** | Limited by human creators | Infinite |
| **IP/Merchandise** | Creator-owned | Platform-owned, licensable |

---

## Features

### Core
- ✅ **AI Character Feed** - Follow AI personalities across 10+ categories
- ✅ **Vertical Video Scroll** - TikTok-style infinite feed
- ✅ **Character Profiles** - Detailed character pages with videos, stats, schedule
- ✅ **Smart Recommendations** - Personalized feed based on followed characters
- ✅ **Engagement Tools** - Like, comment, share, watch-later, notifications
- ✅ **Search & Discovery** - Browse by category, trending characters
- ✅ **Offline Mode** - Download episodes for offline viewing

### AI Characters (v1)
1. **Fashion Model** - Daily outfit showcases, trend reports
2. **Educator** - Coding, languages, history, science lessons
3. **News Anchor** - Daily news digest (60 seconds)
4. **Fitness Coach** - Workouts, nutrition, wellness tips
5. **Comedian** - Daily jokes, sketches, satire
6. **Storyteller** - Short fiction, mysteries, narratives
7. **Town Planner** - Urban design, infrastructure insights
8. **Gaming Streamer** - Game clips, reviews, tips
9. **Chef** - Recipes, cooking hacks, food trends
10. **Travel Guide** - Destination guides, travel hacks

### Monetization (Planned)
- 📺 **Pro Subscription** (₹299/month) - Ad-free, early access, exclusive characters
- 💎 **In-App Currency** - Gems system with rewards
- 🎯 **Targeted Ads** - Smart ad placement for free tier
- 👤 **Character Premium** (v2) - Exclusive episodes per character
- 🎨 **Creator Revenue** (v2) - Users create/customize characters, earn revenue share

---

## Architecture

### Data Models

#### AICharacter
Represents an AI personality/influencer.
```dart
class AICharacter {
  String id;
  String name;
  String category; // fashion_model, teacher, news_anchor, etc.
  String description;
  String profileImageUrl;
  String coverImageUrl;
  String personality; // Bio/character description
  int followers;
  int totalVideoCount;
  double avgEngagementRate;
  bool isVerified;
  bool isOfficial; // Platform-created
  AICharacterStats stats; // Detailed analytics
  List<String> uploadSchedule; // When new videos post
  List<String> videoIds; // Latest video IDs
}
```

#### Video (Updated)
```dart
class Video {
  String id;
  String characterId; // AI character (not user)
  String title;
  String description;
  String videoUrl;
  String thumbnailUrl;
  int duration;
  DateTime createdAt;
  int likes;
  int comments;
  int shares;
  int views;
  String contentType; // 'generated', 'live', 'mixed'
  Map<String, dynamic> generationMetadata; // AI model info
  int episodeNumber; // For serialized content
  String season; // Season/series name
}
```

#### AppUser (Simplified)
```dart
class AppUser {
  String id;
  String email;
  String displayName;
  List<String> followedCharacterIds; // Followed AI characters
  List<String> watchLater; // Saved videos
  int points; // Engagement rewards
  bool hasProAccess;
  Map<String, dynamic> preferences; // Theme, language, etc.
}
```

### API Endpoints

#### Characters
- `GET /characters` - List all characters
- `GET /characters/:id` - Single character
- `GET /characters/categories` - Available categories
- `GET /characters/search?q=...` - Search
- `GET /characters/trending` - Trending characters
- `GET /characters/:id/videos` - Character's videos

#### Videos
- `GET /videos/feed?userId=...` - Personalized feed
- `GET /characters/:id/videos` - Character's video library
- `POST /videos/:id/like` - Like video
- `POST /videos/:id/share` - Share video
- `POST /users/:userId/watch-history` - Log view

#### Users
- `POST /users/:userId/follow` - Follow character
- `GET /users/:userId/followed-characters` - Followed list
- `GET /users/:userId/recommendations` - Personalized videos

### Technology Stack

**Frontend:**
- Framework: `Flutter` (iOS/Android)
- State Management: `Riverpod`
- Networking: `Dio`
- Video: `video_player`
- UI: Material + custom glassmorphism theme

**Backend (Separate):**
- API: FastAPI / Node.js
- Database: Firebase Firestore / PostgreSQL
- Video Storage: Firebase Storage / AWS S3
- Video Generation: Synthesia / RunwayML
- TTS: ElevenLabs
- Image Gen: Stable Diffusion / DALL-E 3

---

## File Structure

```
vidflow_ai/
├── lib/
│   ├── main.dart
│   └── src/
│       ├── config/
│       │   └── theme.dart
│       ├── models/
│       │   ├── ai_character.dart (NEW)
│       │   ├── video.dart (UPDATED)
│       │   └── user.dart (UPDATED)
│       ├── services/
│       │   └── api_service.dart (UPDATED)
│       ├── screens/
│       │   ├── home_screen.dart (UPDATED)
│       │   └── ai_character_profile_screen.dart (NEW)
│       └── widgets/
│           ├── ai_character_card.dart (NEW)
│           └── video_card.dart
├── pubspec.yaml
├── ARCHITECTURE.md
└── README.md
```

---

## Getting Started

### Prerequisites
- Flutter 3.2+
- Dart 3.2+
- iOS/Android emulator or physical device

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/vidflow-ai.git
cd vidflow-ai
```

2. **Install dependencies**
```bash
flutter pub get
```

3. **Generate freezegun models** (required for data models)
```bash
flutter pub run build_runner build --delete-conflicting-outputs
```

4. **Run the app**
```bash
flutter run
```

### Configuration

1. **Firebase Setup** (optional for development)
   - Create Firebase project
   - Add `google-services.json` (Android) and `GoogleService-Info.plist` (iOS)
   - Update `lib/firebase_options.dart`

2. **API Configuration**
   - Update API base URL in `lib/src/services/api_service.dart`
   - Point to your backend API

3. **Theme Customization**
   - Colors in `lib/src/config/theme.dart`
   - Spacing and typography constants

---

## Development Roadmap

### Phase 1: MVP ✅
- [x] Core data models (AICharacter, Video, User)
- [x] API service layer with all endpoints
- [x] Home feed (vertical scroll)
- [x] Character profile screen
- [x] Follow/unfollow system
- [x] AI Character discovery
- [x] Theme & design system
- [ ] Video player optimization
- [ ] Basic analytics tracking

### Phase 2: Enhancement (2-3 weeks)
- [ ] Explore/Discover screen
- [ ] Advanced search & filtering
- [ ] Watch Later functionality
- [ ] Personalized recommendations
- [ ] Share to social media
- [ ] Comments system
- [ ] Character customization (voice, appearance)

### Phase 3: Social (3-4 weeks)
- [ ] User profiles
- [ ] Direct messaging
- [ ] Leaderboards
- [ ] Challenges (user participation)
- [ ] Push notifications
- [ ] Social features

### Phase 4: Monetization (2-3 weeks)
- [ ] Ad integration (AdMob)
- [ ] In-app purchases (IAP)
- [ ] Pro subscription
- [ ] Analytics dashboard
- [ ] Revenue tracking

---

## Screens & Navigation

### HomeScreen
- **For You Tab**: Personalized feed from followed characters
- **Trending Tab**: Discover trending AI characters
- Vertical scroll video player (TikTok-style)
- Character info overlay
- Engagement buttons (like, comment, share)

### AICharacterProfileScreen
- Character cover + profile picture
- Stats (followers, videos, engagement rate)
- **Videos Tab**: Character's latest content
- **About Tab**: Bio, description, tags
- **Schedule Tab**: Upcoming video schedule
- Follow/Subscribe button

### ExploreScreen (Coming Soon)
- Browse by category (Fashion, Education, Comedy, etc.)
- Character cards with quick preview
- Search functionality
- Filter by engagement, followers, etc.

### WatchLaterScreen (Coming Soon)
- Saved videos from all characters
- Organized by character
- Resume from last watch time

---

## API Integration

### Setup Backend Service

The frontend requires a backend API. Here's a minimal example:

```bash
# Backend Example (Node.js + Express)
npm init
npm install express cors dotenv firebase-admin axios

# Create server.js
```

**Key Backend Responsibilities:**
1. Character CRUD & management
2. Video metadata & transcoding
3. User authentication & profile
4. Analytics tracking
5. Recommendation engine
6. Ad serving

See `/backend` folder (if provided) or create your own using the API spec in `ARCHITECTURE.md`.

---

## Configuration & Customization

### Theme Customization
Edit `lib/src/config/theme.dart`:
- Colors: `primaryColor`, `accentColor`, `backgroundColor`
- Typography: Font families, sizes, weights
- Spacing: `xs`, `sm`, `md`, `lg`, `xl`
- Border radius: `radiusSm`, `radiusMd`, `radiusLg`

### API Endpoints
Edit `lib/src/services/api_service.dart`:
- Base URL: Change `baseUrl` constant
- Endpoints: Add new API methods as needed
- Error handling: Customize error messages

### Character Categories
Add new categories in:
1. Backend: Add to character type enum
2. Frontend: Update category filter in `ExploreScreen`
3. Models: Update `AICharacter.category` enum

---

## Testing

### Unit Tests
```bash
flutter test
```

### Integration Tests
```bash
flutter test integration_test/
```

### Widget Tests
```bash
flutter test test/widgets/
```

### Manual Testing Checklist
- [ ] Scroll through video feed
- [ ] Follow/unfollow characters
- [ ] Like/unlike videos
- [ ] View character profiles
- [ ] Search for characters
- [ ] Change theme settings
- [ ] Test offline mode

---

## Performance Optimization

### Video Player
- Preload next video in queue
- Cache thumbnail images
- Limit simultaneous video loads
- Use `LazyFrame` for off-screen videos

### Networking
- Implement request debouncing
- Cache API responses (Riverpod)
- Paginate large lists
- Compress images before upload

### Memory
- Dispose video controllers properly
- Limit cached images
- Use `ListView.builder()` for long lists
- Monitor memory with DevTools

---

## Troubleshooting

### Video Player Not Playing
- Verify video URL is accessible
- Check internet connection
- Ensure `video_player` is initialized
- Check platform-specific permissions

### API Connection Errors
- Verify backend is running
- Check API base URL in `api_service.dart`
- Ensure CORS is enabled (backend)
- Check network connectivity

### Build Errors
```bash
# Clean build
flutter clean
flutter pub get
flutter pub run build_runner build --delete-conflicting-outputs
flutter run
```

### Freezegun Model Issues
```bash
# Regenerate models
flutter pub run build_runner clean
flutter pub run build_runner build --delete-conflicting-outputs
```

---

## Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

---

## License

MIT License - see LICENSE file for details

---

## Support

- 📧 Email: support@vidflow.ai
- 🐛 Report Issues: [GitHub Issues](https://github.com/yourusername/vidflow-ai/issues)
- 💬 Discussions: [GitHub Discussions](https://github.com/yourusername/vidflow-ai/discussions)

---

## Roadmap & Vision

**Short-term (3 months):**
- MVP launch with 10 AI characters
- 100K+ downloads
- Monetization via ads + IAP

**Medium-term (6 months):**
- 50+ AI characters
- User-generated character customization
- Creator revenue sharing
- 1M+ monthly active users

**Long-term (12 months):**
- 200+ AI characters
- Full creator marketplace
- AI character NFTs/merchandise
- International expansion
- 10M+ monthly active users

---

## Competitive Advantages

1. **No Creator Network Effects** - Unlike TikTok, users don't compete with human creators
2. **Predictable Quality** - AI delivers consistent, high-quality content
3. **Infinite Scale** - Generate new characters instantly
4. **Serialization** - Tell ongoing stories (characters evolve)
5. **Merch/IP** - Characters become brands
6. **Global Appeal** - Customize for regional markets
7. **Creator Monetization** - Users can create characters

---

**Build VidFlow AI. Own the AI Creator Economy.** 🚀
