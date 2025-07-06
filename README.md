# STCMS - Hybrid PHP/React CMS Library

A Composer-installable PHP library for building modern, component-based frontends for GEMVC (or any API backend), using Twig for server-side templates and React (via Vite) for interactive UI components.

## Features

- 🚀 **Hybrid Rendering**: Twig for server-side, React for interactive components
- 🔌 **API Integration**: Fetch data from GEMVC or any API using Guzzle
- ⚡ **Modern Caching**: Symfony Cache (APCu/file)
- 🛠️ **CLI Project Init**: Scaffold new projects with `vendor/bin/stcms init`
- 🎨 **Component-based UI**: React components in `/assets/js/components/`, bundled with Vite
- 🗂️ **Multi-language Support**: Easily add new languages
- 🔒 **Config via .env**: Symfony Dotenv for environment config
- 🧩 **Extensible**: Easy for both PHP and frontend devs

## Quick Start

### 1. Install via Composer
```bash
composer require gemvc/stcms
```

### 2. Initialize a New Project
```bash
vendor/bin/stcms init
```

### 3. Build Frontend Assets (React via Vite)
```bash
npm install
npx vite build
```

### 4. Configure Environment
Edit `.env` for API base URL, cache, etc.

### 5. Start Developing
- **Twig templates** in `/templates/`
- **React components** in `/assets/js/components/`
- **API calls** via Guzzle in PHP

## Project Structure
```
/
├── src/                    # PHP library code
│   ├── Core/               # Core classes (Cache, ApiClient, etc.)
│   └── Command/            # CLI commands
├── templates/              # Twig templates (layouts, pages, components)
├── assets/
│   ├── js/
│   │   ├── components/     # React components (JSX)
│   │   └── app.jsx         # Main React entry
│   └── css/                # CSS (optional, Tailwind via CDN or Vite)
├── public/
│   └── assets/js/          # Vite build output
├── .env                    # Config
├── vite.config.js          # Vite config
├── composer.json           # Composer config
└── bin/stcms               # CLI entry point
```

## How It Works
- **Twig renders main pages**; React components are mounted where needed
- **API data fetched via Guzzle** (with Symfony Cache)
- **Frontend devs build React components in `/assets/js/components/`**
- **Vite bundles JS for use in templates**
- **Config and cache are environment-driven**

## Example: Hybrid Rendering

Twig template:
```twig
<div id="user-profile-root" data-user="{{ user|json_encode }}" {% if jwt %}data-jwt="{{ jwt }}"{% endif %}></div>
<script src="/assets/js/app.js"></script>
```

React entry (app.jsx):
```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';
import UserProfile from './components/UserProfile';

const el = document.getElementById('user-profile-root');
if (el) {
  const user = JSON.parse(el.dataset.user);
  const jwt = el.dataset.jwt; // Only present if authenticated
  createRoot(el).render(<UserProfile user={user} jwt={jwt} />);
}
```

## Authentication Flow & Security
- **JWT is only exposed to React if the user is authenticated** (JWT is present in PHP session).
- **If not authenticated, no JWT is exposed**—React knows to show login or restrict access.
- **React components use the JWT for API requests** (e.g., via Axios/fetch, in Authorization header).
- **JWT is never generated or verified in the frontend**—all JWT logic is handled by the backend (GEMVC API).
- **Session management and login/logout handled by PHP backend.**
- **Best practice:** Always validate JWTs on the backend for every API request.

## Benefits
- ✅ Clean separation of backend, templates, and frontend components
- ✅ Easy for both PHP and React developers
- ✅ Fast, SEO-friendly, and interactive
- ✅ Works on most hosting (APCu/file cache)
- ✅ Extensible and maintainable

## For PHP Developers
- Use Twig for layouts, pages, and partials
- Fetch API data with Guzzle (and cache it)
- Pass data to React components via JSON in the DOM
- Expose JWT to React only if authenticated

## For React Developers
- Build components in `/assets/js/components/`
- Use Vite for fast dev/build
- Mount components anywhere in Twig templates
- Use JWT (if present) for authenticated API requests

## Contributing
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License
MIT

## Support

- **Documentation**: `/en/docs`
- **Issues**: GitHub Issues
- **Discussions**: GitHub Discussions

## Changelog

### Version 1.0.0
- Initial release
- Multi-language support
- Template system
- File-based caching
- SEO optimization
- Responsive design

---

**STCMS** - Making static websites simple and powerful! 🚀 