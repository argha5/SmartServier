# Servier Medical Art — Complete Image Database & App Integration Guide

Welcome to the **Servier Medical Art** image repository! This project contains **all 990 high-resolution medical illustrations** converted directly from the official 49 PowerPoint kits available on [smart.servier.com](https://smart.servier.com/).

---

## 🌐 Official Servier Website Taxonomy & Mapping

On [smart.servier.com](https://smart.servier.com/), medical illustrations are grouped under 5 primary navigation trees and 11 core categories. Every single downloadable PowerPoint kit on the official website is 100% included in this repository:

| Primary Web Category | Subcategories / Medical Fields | Mapped Image Kits | Total Images |
| :--- | :--- | :--- | :---: |
| **Anatomy & Human Body** | Heart, Arteries, Veins, Blood, Digestive, Locomotor, Nervous, Reproductive, Respiratory, Urinary, Visual | `smart-arteries-*`, `smart-heart-*`, `smart-veins`, `smart-digestive-system`, `smart-bones`, `smart-muscles`, `smart-nervous-system`, `smart-ophthalmology`, etc. | **540** |
| **Cellular Biology** | Cell membrane, Intracellular, Genetics, Lipids, Nucleic acids, Receptors & Channels, Tissues | `smart-cell-membrane`, `smart-genetics`, `smart-lipids`, `smart-nucleic-acids`, `smart-receptors-channels`, `smart-tissues` | **105** |
| **Infectiology** | Micology, Parasitology, Virology, Cell Culture | `smart-infectiology`, `smart-parasitology`, `smart-microbiology-cell-culture` | **65** |
| **General Items & Equipment** | Animals, Clothes, Equipment, Food, People, Scientific Graphs, World Maps | `smart-animals`, `smart-medical-equipment`, `smart-emergency-equipment`, `smart-dietetics`, `smart-people`, `smart-scientific-graphs`, `smart-world-maps` | **210** |
| **Medical Specialties** | Cardiology, Dermatology, Embryology, Endocrinology, Gastroenterology, Neurology, Oncology, Pulmonology, Urology | `smart-dermatology`, `smart-endocrinology`, `smart-oncology`, `smart-respiratory-system`, `smart-urinary-system`, etc. | **70** |

---

## 📁 Repository Directory Structure

```
D:\SmartServier\
├── categories.json               # Index of 11 categories + Website Navigation Taxonomy
├── smart_servier_images.json      # Master database containing all 990 images with search tags
├── README.md                      # Developer documentation (this file)
└── images/                        # High-resolution PNG images grouped by category & kit
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

Push this repository to your GitHub account (`https://github.com/YOUR_USERNAME/YOUR_REPO_NAME`). All images and JSON manifests will immediately be accessible via GitHub's CDN:

### Base URL Format:
```
https://raw.githubusercontent.com/<YOUR_GITHUB_USERNAME>/<YOUR_REPO_NAME>/main/
```

### Direct Endpoints:
- **Categories API Index:**
  `https://raw.githubusercontent.com/<YOUR_USERNAME>/<REPO>/main/categories.json`
- **Master Image Database (Search & Filter):**
  `https://raw.githubusercontent.com/<YOUR_USERNAME>/<REPO>/main/smart_servier_images.json`
- **Sample Medical Illustration (Angioplasty 1):**
  `https://raw.githubusercontent.com/<YOUR_USERNAME>/<REPO>/main/images/heart-circulatory-system/smart-arteries-atherothrombosis/slide-020.png`

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
```

### 2. React / React Native Example

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
```

---

## ⚖️ License & Attribution Requirements

All medical art assets are provided by **Servier Medical Art** (Les Laboratoires Servier) under the **[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)** license.

### Required Credit in your Mobile / Web App:
> *"Medical illustrations provided by Servier Medical Art (https://smart.servier.com/), licensed under CC BY 4.0."*
