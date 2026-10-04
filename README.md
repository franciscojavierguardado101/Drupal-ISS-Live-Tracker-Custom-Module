# Drupal ISS Live Tracker Custom Module

A Drupal 11 custom module that provides an `iss_tracker` paragraph type, enabling editors to place a live International Space Station tracker on any page via the CMS. The Next.js frontend that renders the live map, crew list, and Wikipedia bios lives at: https://github.com/franciscojavierguardado101/Frontend-Typescript-ISS-Tracker

## What it does

- Registers an `iss_tracker` paragraph type so editors can drop the ISS tracker onto any landing page from the Drupal admin
- Provides an optional label field (`field_iss_label`) for editors to customize the section heading
- Works as a headless paragraph: Drupal stores and delivers the component data via JSON:API, and the Next.js frontend handles all rendering

## What the frontend renders

Once this module is enabled and the paragraph is placed on a page, the Next.js frontend displays:

- Live Leaflet map with the ISS position updated every 5 seconds
- Ground track polyline showing the ISS path (last 60 positions)
- Footprint circle showing the ISS visibility area on the ground
- Follow / Free toggle to lock or unlock the map camera on the ISS
- Live crew list pulled from a public space station API
- Clickable crew names that load a Wikipedia bio panel with photo and summary

## APIs used (no keys required)

| Data | Source |
|------|--------|
| ISS position | wheretheiss.at REST API |
| Crew list | corquaid.github.io/international-space-station-APIs |
| Crew bios | Wikipedia REST API |

## Installation

Requires Drupal 10 or 11 with the `paragraphs` module enabled.

```bash
cp -r francisco_iss_tracker /path/to/web/modules/custom/
drush en francisco_iss_tracker -y
drush cr
```

## File structure

```
francisco_iss_tracker/
  francisco_iss_tracker.info.yml     # Module definition and dependencies
  config/install/
    paragraphs.paragraphs_type.iss_tracker.yml
    field.storage.paragraph.field_iss_label.yml
    field.field.paragraph.iss_tracker.field_iss_label.yml
    core.entity_form_display.paragraph.iss_tracker.default.yml
    core.entity_view_display.paragraph.iss_tracker.default.yml
```

## Stack

- Drupal 11 (headless, Pantheon)
- PHP 8.2
- Paragraphs module
- Next.js 16 frontend on Vercel
