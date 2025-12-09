# Talisman — Asymmetrical Content Grid

## Overview
Talisman is a complex grid layout component that combines multiple content types (avatars, images, statistics, product showcases) in an asymmetrical 3×2 arrangement. Designed for agency portfolios and brand showcases, it creates visual interest through varied content areas within a cohesive grid system.

## Live Demo

[View Talisman](https://thisislefa.github.io/Talisman)



## Technology
- **HTML5**: Semantic structure with CSS grid areas
- **CSS3**: CSS Grid with custom grid-template-areas, CSS Custom Properties
- **Google Fonts**: Inter (400-700 weights)
- **No JavaScript**: Pure CSS implementation
- **Pexels/Pravatar**: High-quality placeholder imagery



## Grid Architecture

### Layout Structure
```
Grid Areas:
┌───────────┬───────────┬───────────┐
│ left-top  │  center   │   right   │
│           │           │           │
├───────────┤           │           │
│ left-     │           │           │
│ bottom    │           │           │
└───────────┴───────────┴───────────┘
```

### CSS Grid Implementation
```css
.fbx-s2-grid-wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: auto auto;
    grid-template-areas:
        "left-top center right"
        "left-bottom center right";
    gap: 15px;
}
```


## Integration

### Basic Implementation
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="talisman.css">
</head>
<body>
    <!-- Talisman component -->
</body>
</html>
```

### React Component
```jsx
import './talisman.css';

function TalismanGrid({ 
    heading = "Crafting bold ideas into exceptional digital experiences",
    avatars = [
        "https://i.pravatar.cc/100?img=47",
        "https://i.pravatar.cc/100?img=33",
        "https://i.pravatar.cc/100?img=5"
    ],
    avatarText = "Sustainable creativity, timeless appeal.",
    highlightText = "creativity",
    stats = {
        number: "95%",
        label: "Customer satisfaction rate"
    },
    product = {
        image: "https://images.pexels.com/photos/7797734/pexels-photo-7797734.jpeg",
        title: "We give brands a visual voice",
        description: "Our innovative approach ensures your brand stands out..."
    }
}) {
    return (
        <section className="fbx-s2-container">
            <h2 className="fbx-s2-heading">{heading}</h2>
            
            <div className="fbx-s2-grid-wrapper">
                {/* Top-left: Avatars */}
                <div className="fbx-s2-card fbx-s2-card--white fbx-s2-card-avatars">
                    <div className="fbx-s2-avatar-group">
                        {avatars.map((avatar, index) => (
                            <img key={index} src={avatar} alt={`User Avatar ${index + 1}`} className="fbx-s2-avatar" />
                        ))}
                    </div>
                    <p className="fbx-s2-avatar-text">
                        {avatarText.replace(highlightText, `<span class="fbx-s2-text-highlight">${highlightText}</span>`)}
                    </p>
                </div>
                
                {/* Bottom-left: Credit card image */}
                <div className="fbx-s2-card fbx-s2-card-credit">
                    <img src="https://images.pexels.com/photos/19314870/pexels-photo-19314870.jpeg" alt="Hand holding a yellow credit card" />
                </div>
                
                {/* Center: Astronaut with stats */}
                <div className="fbx-s2-card fbx-s2-card-astronaut">
                    <img src="https://images.pexels.com/photos/8000622/pexels-photo-8000622.jpeg" alt="Astronaut sitting on a bench under an umbrella" />
                    <div className="fbx-s2-astronaut-content">
                        <span className="fbx-s2-stat-number">{stats.number}</span>
                        <span className="fbx-s2-stat-label">{stats.label}</span>
                    </div>
                </div>
                
                {/* Right: Product showcase */}
                <div className="fbx-s2-card fbx-s2-card--white fbx-s2-card-products">
                    <div className="fbx-s2-product-image-container">
                        <img src={product.image} alt={product.title} className="fbx-s2-product-image" />
                    </div>
                    <h3 className="fbx-s2-product-heading">{product.title}</h3>
                    <p className="fbx-s2-product-description">{product.description}</p>
                </div>
            </div>
        </section>
    );
}
```

### WordPress Integration
```php
function talisman_grid_shortcode($atts) {
    $atts = shortcode_atts([
        'heading' => 'Crafting bold ideas into exceptional digital experiences',
        'stat_number' => '95%',
        'stat_label' => 'Customer satisfaction rate',
        'product_title' => 'We give brands a visual voice',
        'product_desc' => 'Our innovative approach ensures your brand stands out in a crowded market...'
    ], $atts);
    
    ob_start();
    ?>
    <section class="fbx-s2-container">
        <h2 class="fbx-s2-heading"><?php echo esc_html($atts['heading']); ?></h2>
        
        <div class="fbx-s2-grid-wrapper">
            <!-- Avatar card -->
            <div class="fbx-s2-card fbx-s2-card--white fbx-s2-card-avatars">
                <div class="fbx-s2-avatar-group">
                    <img src="https://i.pravatar.cc/100?img=47" alt="User Avatar 1" class="fbx-s2-avatar">
                    <img src="https://i.pravatar.cc/100?img=33" alt="User Avatar 2" class="fbx-s2-avatar">
                    <img src="https://i.pravatar.cc/100?img=5" alt="User Avatar 3" class="fbx-s2-avatar">
                </div>
                <p class="fbx-s2-avatar-text">
                    Sustainable <span class="fbx-s2-text-highlight">creativity</span>,<br>
                    timeless appeal.
                </p>
            </div>
            
            <!-- Credit card image -->
            <div class="fbx-s2-card fbx-s2-card-credit">
                <img src="https://images.pexels.com/photos/19314870/pexels-photo-19314870.jpeg" alt="Hand holding a credit card">
            </div>
            
            <!-- Stat card -->
            <div class="fbx-s2-card fbx-s2-card-astronaut">
                <img src="https://images.pexels.com/photos/8000622/pexels-photo-8000622.jpeg" alt="Astronaut">
                <div class="fbx-s2-astronaut-content">
                    <span class="fbx-s2-stat-number"><?php echo esc_html($atts['stat_number']); ?></span>
                    <span class="fbx-s2-stat-label"><?php echo esc_html($atts['stat_label']); ?></span>
                </div>
            </div>
            
            <!-- Product card -->
            <div class="fbx-s2-card fbx-s2-card--white fbx-s2-card-products">
                <div class="fbx-s2-product-image-container">
                    <img src="https://images.pexels.com/photos/7797734/pexels-photo-7797734.jpeg" alt="Cosmetic products" class="fbx-s2-product-image">
                </div>
                <h3 class="fbx-s2-product-heading"><?php echo esc_html($atts['product_title']); ?></h3>
                <p class="fbx-s2-product-description"><?php echo esc_html($atts['product_desc']); ?></p>
            </div>
        </div>
    </section>
    <?php
    return ob_get_clean();
}
add_shortcode('talisman_grid', 'talisman_grid_shortcode');
```


## Customization

### CSS Custom Properties
```css
:root {
    --fbx-s2-font-family: 'Inter', sans-serif;
    --fbx-s2-bg-color: #f5f5f7;
    --fbx-s2-text-color-primary: #1d1d1f;
    --fbx-s2-text-color-secondary: #6e6e73;
    --fbx-s2-card-bg-white: #ffffff;
    --fbx-s2-border-radius: 8px;
    --fbx-s2-grid-gap: 15px;
    --fbx-s2-stat-color: #ffffff;
    --fbx-s2-highlight-color: #1d1d1f;
}

/* Dark mode variant */
.talisman-dark {
    --fbx-s2-bg-color: #1d1d1f;
    --fbx-s2-text-color-primary: #f5f5f7;
    --fbx-s2-card-bg-white: #2d2d2f;
    --fbx-s2-text-color-secondary: #a1a1a6;
}
```

### Grid Layout Variations
```css
/* Alternative 4-column layout */
.fbx-s2-grid-wrapper.four-col {
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-template-rows: auto auto;
    grid-template-areas:
        "top-left top-left center right"
        "bottom-left bottom-left center right";
}

/* Stacked layout (mobile-first) */
.fbx-s2-grid-wrapper.stacked {
    grid-template-columns: 1fr;
    grid-template-rows: repeat(4, auto);
    grid-template-areas:
        "left-top"
        "left-bottom"
        "center"
        "right";
}

/* Custom area assignments */
.fbx-s2-grid-wrapper.custom-areas {
    grid-template-areas:
        "stat product product"
        "avatar avatar image";
}
```

### Component Variations
```css
/* Avatar stack with different sizes */
.fbx-s2-avatar-group.large .fbx-s2-avatar {
    width: 64px;
    height: 64px;
}

.fbx-s2-avatar-group.small .fbx-s2-avatar {
    width: 36px;
    height: 36px;
    border-width: 2px;
}

/* Stat card with gradient overlay */
.fbx-s2-card-astronaut::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
}

/* Product card with hover effect */
.fbx-s2-card-products:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 24px rgba(0,0,0,0.1);
}

.fbx-s2-card-products:hover .fbx-s2-product-image {
    transform: scale(1.05);
}
```

### Responsive Enhancements
```css
@media (max-width: 768px) {
    .fbx-s2-heading {
        font-size: 32px;
        margin-bottom: 40px;
    }
    
    .fbx-s2-stat-number {
        font-size: 60px;
    }
    
    .fbx-s2-product-heading {
        font-size: 24px;
    }
    
    /* Stack avatars horizontally on mobile */
    .fbx-s2-avatar-group {
        margin-right: 0;
        margin-bottom: 16px;
    }
    
    .fbx-s2-avatar:not(:first-child) {
        margin-left: -12px;
    }
}

@media (min-width: 1025px) and (max-width: 1200px) {
    .fbx-s2-container {
        padding: 60px 40px;
    }
    
    .fbx-s2-heading {
        font-size: 48px;
        max-width: 700px;
    }
}
```

---

## Responsive Behavior

### Breakpoints
- **Desktop (1025px+)**: Full 3×2 grid with complex areas
- **Tablet (769px-1024px)**: Reduced font sizes, adjusted spacing
- **Mobile (≤768px)**: Single column stack, simplified layout

### Mobile-First Overrides
```css
/* Default: mobile layout */
.fbx-s2-grid-wrapper {
    grid-template-columns: 1fr;
    grid-template-areas:
        "left-top"
        "left-bottom"
        "center"
        "right";
    gap: 20px;
}

/* Desktop overrides */
@media (min-width: 1025px) {
    .fbx-s2-grid-wrapper {
        grid-template-columns: 1fr 1fr 1fr;
        grid-template-areas:
            "left-top center right"
            "left-bottom center right";
        gap: 15px;
    }
}
```

### Touch Optimizations
```css
@media (hover: none) and (pointer: coarse) {
    .fbx-s2-card {
        min-height: 200px; /* Larger touch targets */
    }
    
    .fbx-s2-avatar {
        min-width: 56px;
        min-height: 56px;
    }
    
    .fbx-s2-product-image-container {
        padding: 20px 0; /* Larger touch area */
    }
}
```


## Performance

### Optimizations
- **CSS Grid**: Efficient layout rendering
- **CSS Custom Properties**: Easy theming without recalculation
- **Optimized images**: Pexels CDN with automatic optimization
- **Font loading**: `font-display: swap` for Inter font
- **Minimal animations**: Only essential transitions

### Loading Strategy
```html
<!-- Preload critical resources -->
<link rel="preload" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" as="style">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Lazy load non-critical images -->
<img 
    src="placeholder.jpg"
    data-src="https://images.pexels.com/photos/8000622/pexels-photo-8000622.jpeg"
    class="fbx-s2-card-astronaut-img lazy"
    alt="Astronaut"
    loading="lazy"
    width="600"
    height="800"
>
```


## Accessibility

### WCAG Compliance
- **Semantic HTML**: section, h2, h3 elements
- **Color contrast**: 4.5:1 minimum ratios
- **Image alt text**: Descriptive alt attributes
- **Focus indicators**: Visible focus states
- **Text scaling**: Supports browser zoom up to 200%

### ARIA Enhancements
```html
<section class="fbx-s2-container" aria-label="Digital Experiences Showcase">
    <h2 class="fbx-s2-heading" id="section-heading">Crafting bold ideas...</h2>
    
    <div class="fbx-s2-grid-wrapper" role="region" aria-labelledby="section-heading">
        <!-- Avatar card with aria-label -->
        <div class="fbx-s2-card fbx-s2-card-avatars" role="group" aria-label="Team members">
            <!-- Avatar images with alt text -->
        </div>
        
        <!-- Stat card with aria-live -->
        <div class="fbx-s2-card fbx-s2-card-astronaut" aria-live="polite">
            <span class="fbx-s2-stat-number" aria-label="95 percent">95%</span>
            <span class="fbx-s2-stat-label">Customer satisfaction rate</span>
        </div>
    </div>
</section>
```

### Accessibility CSS
```css
/* Focus management */
.fbx-s2-card:focus {
    outline: 3px solid #0066cc;
    outline-offset: 2px;
}

/* Reduced motion support */
@media (prefers-reduced-motion: reduce) {
    .fbx-s2-card,
    .fbx-s2-product-image {
        transition: none;
    }
}

/* High contrast mode */
@media (prefers-contrast: high) {
    .fbx-s2-card--white {
        border: 2px solid currentColor;
    }
    
    .fbx-s2-text-highlight {
        text-decoration: underline;
    }
}
```


## Browser Support

| Browser | Version | CSS Grid | Custom Properties |
|---------|---------|----------|-------------------|
| Chrome  | 57+     | ✓        | ✓                 |
| Firefox | 52+     | ✓        | ✓                 |
| Safari  | 10.1+   | ✓        | ✓                 |
| Edge    | 16+     | ✓        | ✓                 |

### Fallback Strategy
```css
/* Flexbox fallback for older browsers */
.fbx-s2-grid-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
}

.fbx-s2-card-avatars,
.fbx-s2-card-credit,
.fbx-s2-card-astronaut,
.fbx-s2-card-products {
    flex: 1 1 calc(50% - 15px);
    margin-bottom: 15px;
}

/* Grid override for modern browsers */
@supports (display: grid) {
    .fbx-s2-grid-wrapper {
        display: grid;
    }
    
    .fbx-s2-card-avatars,
    .fbx-s2-card-credit,
    .fbx-s2-card-astronaut,
    .fbx-s2-card-products {
        flex: none;
        margin-bottom: 0;
    }
}
```


## SEO Best Practices

### Semantic Structure
- Proper heading hierarchy (h2 > h3)
- Descriptive alt text for all images
- Logical content flow in grid areas
- Mobile-responsive design

### Performance SEO
- Fast loading with minimal resources
- Optimized images with appropriate sizes
- Clean CSS with efficient selectors
- No render-blocking JavaScript


## Quick Start

1. **Include CSS and fonts**
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="talisman.css">
```

2. **Add HTML structure**
```html
<section class="fbx-s2-container">
    <h2 class="fbx-s2-heading">Your Heading</h2>
    <div class="fbx-s2-grid-wrapper">
        <!-- Grid items -->
    </div>
</section>
```

3. **Customize content**
- Update image URLs
- Modify text content
- Adjust colors via CSS custom properties
- Change grid areas as needed


## Troubleshooting

### Common Issues
1. **Grid not aligning**: Check browser support for CSS Grid
2. **Images not loading**: Verify URLs and CORS headers
3. **Fonts not displaying**: Ensure Google Fonts link is correct
4. **Layout breaks on mobile**: Test responsive breakpoints

### Debugging Tips
```css
/* Add debugging outlines */
.debug .fbx-s2-grid-wrapper * {
    outline: 1px solid red !important;
}

.debug .fbx-s2-card {
    background: rgba(255, 0, 0, 0.1) !important;
}
```


**Talisman** — Complex asymmetrical grid for showcasing diverse content types with visual impact.

