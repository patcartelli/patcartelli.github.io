# Studio Cartelli

Personal website hosted on GitHub Pages with custom domain.

## Live Site

- GitHub Pages: [https://patcartelli.github.io](https://patcartelli.github.io)
- Custom Domain: [https://studiocartelli.com](https://studiocartelli.com)

## Setup

This site is automatically deployed via GitHub Pages from the `main` branch.

### Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/patcartelli/patcartelli.github.io.git
   cd patcartelli.github.io
   ```

2. Open `index.html` in your browser to preview locally.

### Deployment

Changes pushed to the `main` branch are automatically deployed to GitHub Pages.

```bash
git add .
git commit -m "Update site"
git push origin main
```

## DNS Configuration

To use the custom domain `studiocartelli.com`, configure the following DNS records at your domain registrar:

### Option 1: Apex Domain (studiocartelli.com)

Add the following A records:

```
Type: A
Name: @
Value: 185.199.108.153

Type: A
Name: @
Value: 185.199.109.153

Type: A
Name: @
Value: 185.199.110.153

Type: A
Name: @
Value: 185.199.111.153
```

### Option 2: Subdomain (www.studiocartelli.com)

Add a CNAME record:

```
Type: CNAME
Name: www
Value: patcartelli.github.io
```

### Both Options

For the best setup, configure both the apex domain and www subdomain as described above.

## Features

- Responsive design that works on mobile and desktop
- Clean, modern aesthetic
- Fast loading and optimized performance
- HTTPS enabled via GitHub Pages
- Custom domain support

## Technology Stack

- HTML5
- CSS3
- GitHub Pages
- Custom Domain (studiocartelli.com)

## License

© 2026 Studio Cartelli. All rights reserved.
