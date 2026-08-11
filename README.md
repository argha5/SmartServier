# Servier Medical Art — Developer Integration Guide & Image Database

Welcome to the **Servier Medical Art** image repository! This project contains 990 high-resolution medical illustrations and slides converted from the official [Servier Medical Art](https://smart.servier.com/) PowerPoint kits, organized into 11 medical categories.

---

## 📁 Repository & Directory Structure

```
.
├── categories.json               # Index of all 11 categories, kits, and cover images
├── smart_servier_images.json      # Master database containing all 990 images with search tags
├── README.md                      # Developer documentation (this file)
└── images/                        # Image assets organized by category & kit
    ├── bones/
    ├── cellular-biology-histology/
    ├── general-items/
    ├── heart-circulatory-system/
    ├── infectiology/
    ├── laboratory-equipment/
    ├── medical-practice/
    ├── neurology/
    ├── other-medical-fields/
    ├── physiology/
    └── risk-factors/
```

---

## 🌐 How to Use Raw GitHub URLs in Your App

When you push this repository to GitHub, all images and JSON files become directly accessible over GitHub's raw content CDN:

### Base URL Format:
```
https://raw.githubusercontent.com/<YOUR_GITHUB_USERNAME>/<YOUR_REPO_NAME>/main/
```

### Example URLs:
- **Categories API Index:**
  `https://raw.githubusercontent.com/<YOUR_USERNAME>/<REPO>/main/categories.json`
- **Master Image Database:**
  `https://raw.githubusercontent.com/<YOUR_USERNAME>/<REPO>/main/smart_servier_images.json`
- **Sample Image (Angioplasty 1):**
  `https://raw.githubusercontent.com/<YOUR_USERNAME>/<REPO>/main/images/heart-circulatory-system/smart-arteries-atherothrombosis/slide-020.png`

---

## 📊 JSON Schemas

### 1. `categories.json` (Category Index for App Home / Category List)

```json
{
  "metadata": {
    "title": "Servier Medical Art Categories Index",
    "totalCategories": 11,
    "totalKits": 49,
    "totalImages": 990
  },
  "categories": [
    {
      "id": "heart-circulatory-system",
      "name": "Heart & Circulatory System",
      "icon": "🫀",
      "totalKits": 9,
      "totalImages": 244,
      "kits": [
        {
          "id": "smart-arteries-atherothrombosis",
          "title": "Arteries & Atherothrombosis",
          "sourcePptx": "SMART-Arteries-atherothrombosis.pptx",
          "imageFolder": "images/heart-circulatory-system/smart-arteries-atherothrombosis",
          "imageCount": 28,
          "coverImage": "images/heart-circulatory-system/smart-arteries-atherothrombosis/slide-001.png"
        }
      ]
    }
  ]
}
```

### 2. `smart_servier_images.json` (Master Image Database)

```json
{
  "metadata": {
    "title": "Servier Medical Art Image Database",
    "license": "Creative Commons Attribution 4.0 International (CC BY 4.0)",
    "totalCategories": 11,
    "totalDecks": 49,
    "totalImages": 990
  },
  "images": [
    {
      "id": "smart-arteries-atherothrombosis-slide-020",
      "deck": "SMART-Arteries-atherothrombosis",
      "mainCategory": "Heart & Circulatory System",
      "mainCategorySlug": "heart-circulatory-system",
      "category": "Arteries & Atherothrombosis",
      "categorySlug": "smart-arteries-atherothrombosis",
      "slideNumber": 20,
      "image": "images/heart-circulatory-system/smart-arteries-atherothrombosis/slide-020.png",
      "title": "Angioplasty (1)",
      "description": "Angioplasty (1)...",
      "tags": ["heart-circulatory-system", "smart-arteries-atherothrombosis", "arteries-atherothrombosis"]
    }
  ]
}
```

---

## 💻 Developer Code Examples

### 1. Flutter (Dart) Example

```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

class ServierArtService {
  static const String baseUrl = 
      'https://raw.githubusercontent.com/YOUR_USER/YOUR_REPO/main/';

  static Future<List<dynamic>> fetchCategories() async {
    final response = await http.get(Uri.parse('${baseUrl}categories.json'));
    if (response.statusCode == 200) {
      final data = json.decode(response.body);
      return data['categories'];
    }
    throw Exception('Failed to load categories');
  }

  static String getImageUrl(String relativePath) {
    return '$baseUrl$relativePath';
  }
}

// Widget to render Category Card
Widget buildCategoryCard(Map<String, dynamic> category) {
  final coverUrl = ServierArtService.getImageUrl(category['kits'][0]['coverImage']);
  return Card(
    child: Column(
      children: [
        Image.network(coverUrl, height: 120, fit: BoxFit.cover),
        ListTile(
          title: Text('${category["icon"]} ${category["name"]}'),
          subtitle: Text('${category["totalImages"]} Medical Images'),
        ),
      ],
    ),
  );
}
```

### 2. React / React Native (JavaScript/TypeScript) Example

```typescript
const BASE_URL = "https://raw.githubusercontent.com/YOUR_USER/YOUR_REPO/main/";

export async function fetchMedicalCategories() {
  const res = await fetch(`${BASE_URL}categories.json`);
  const data = await res.json();
  return data.categories;
}

export function getServierImageUrl(relativePath: string): string {
  return `${BASE_URL}${relativePath}`;
}

// Usage in React component
export function CategoryItem({ category }: { category: any }) {
  const coverUrl = getServierImageUrl(category.kits[0].coverImage);
  return (
    <div className="category-card">
      <img src={coverUrl} alt={category.name} />
      <h3>{category.icon} {category.name}</h3>
      <p>{category.totalImages} images</p>
    </div>
  );
}
```

### 3. Android (Kotlin) Example

```kotlin
val baseUrl = "https://raw.githubusercontent.com/YOUR_USER/YOUR_REPO/main/"

fun getFullImageUrl(relativePath: String): String {
    return "$baseUrl$relativePath"
}

// Loading image with Glide / Coil
Glide.with(context)
    .load(getFullImageUrl("images/heart-circulatory-system/smart-arteries-atherothrombosis/slide-020.png"))
    .into(imageView)
```

---

## ⚖️ License & Attribution Requirements

All medical art assets are provided by **Servier Medical Art** (Les Laboratoires Servier) under the **[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)** license.

### Required Credit in your Mobile / Web App:
> *"Medical illustrations provided by Servier Medical Art (https://smart.servier.com/), licensed under CC BY 4.0."*
