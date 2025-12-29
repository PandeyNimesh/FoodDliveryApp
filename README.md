A modern, responsive food delivery application inspired by Swiggy, built with React, JavaScript, and Tailwind CSS. This application provides a seamless user experience for browsing restaurants, viewing menus, searching for dishes, and managing a shopping cart.

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Architecture](#architecture)
- [Components Overview](#components-overview)
- [State Management](#state-management)
- [API Integration](#api-integration)
- [Contributing](#contributing)

## ✨ Features

### Core Functionality
- **Restaurant Browsing**: View a comprehensive list of restaurants with ratings and delivery times
- **Menu Exploration**: Browse detailed restaurant menus with categories and subcategories
- **Search Functionality**: Search for specific dishes within a restaurant's menu
- **Cart Management**: Add, increment, and decrement items in shopping cart
- **Dietary Filters**: Filter menu items by vegetarian and non-vegetarian options
- **Multiple Services**: Access food delivery, grocery shopping (Instamart), and dine-out options

### User Experience
- **Shimmer Effect**: Smooth loading placeholders while fetching data
- **Responsive Design**: Mobile-first design using Tailwind CSS
- **Dynamic Routing**: Seamless navigation between pages
- **Real-time Cart Updates**: Live cart counter across all pages
- **Hover Animations**: Interactive UI elements with smooth transitions

## 🛠️ Tech Stack

### Frontend
- **React 18** - UI library with hooks and functional components
- **React Router** - Client-side routing and navigation
- **Tailwind CSS** - Utility-first CSS framework for styling
- **Parcel** - Zero-configuration bundler for fast builds

### State Management
- **Redux Toolkit** - Simplified Redux for global state management
- **React Redux** - Official React bindings for Redux

### APIs
- **Swiggy API** - Restaurant and menu data (via CORS proxy)

## 📁 Project Structure

```
FoodApp/
├── src/
│   ├── App.js                    # Main app component with routing
│   ├── index.html                # HTML template
│   ├── index.css                 # Global styles
│   ├── Components/
│   │   ├── Home.js              # Landing page
│   │   ├── Header.js            # Main header with navigation
│   │   ├── Restaurant.js        # Restaurant listing page
│   │   ├── RestaurantMenu.js    # Restaurant menu with filters
│   │   ├── SearchFood.js        # Search interface for dishes
│   │   ├── Checkout.js          # Shopping cart page
│   │   ├── SecondaryHome.js     # Layout for restaurant pages
│   │   ├── RestHeader.js        # Header for restaurant pages
│   │   ├── RestCard.js          # Restaurant card component
│   │   ├── MenuCard.js          # Menu category component
│   │   ├── RestInfo.js          # Individual menu item
│   │   ├── FoodOption.js        # Food category grid
│   │   ├── FoodCard.js          # Food category card
│   │   ├── GroceryOption.js     # Grocery section
│   │   ├── GroceryCard.js       # Grocery category card
│   │   ├── DineOption.js        # Dine-out section
│   │   ├── DineCard.js          # Dine-out restaurant card
│   │   └── Shimmer.js           # Loading skeleton
│   ├── Stored/
│   │   ├── stores.js            # Redux store configuration
│   │   └── CartSlicer.js        # Cart slice with reducers
│   └── Utils/
│       ├── FoodData.js          # Static food category data
│       ├── Grocery.js           # Static grocery data
│       └── DineData.js          # Static dine-out data
├── docs/                         # Production build
├── package.json                  # Dependencies and scripts
└── README.md                     # This file
```

## 🚀 Installation

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn

### Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd FoodApp
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start development server**
   ```bash
   npm start
   ```

4. **Build for production**
   ```bash
   npm run build
   ```

The app will be available at `http://localhost:1234` (or the port Parcel assigns).

## 💻 Usage

### Browsing Restaurants
1. Navigate to the home page
2. Click on "Food" service option
3. Browse through the list of available restaurants
4. Click on any restaurant card to view its menu

### Adding Items to Cart
1. Open a restaurant menu
2. Browse through menu categories
3. Click "ADD" button on any item
4. Use "+" and "-" buttons to adjust quantity
5. View cart count in the header

### Filtering Menu Items
1. On the restaurant menu page
2. Click "Veg" button to show only vegetarian items
3. Click "Non veg" button to show only non-vegetarian items
4. Click again to remove filter

### Searching for Dishes
1. On the restaurant menu page
2. Click "Search for Dishes" at the top
3. Type the dish name in the search bar
4. Results will be filtered in real-time

## 🏗️ Architecture

### Component Hierarchy

```
App
├── Provider (Redux)
├── BrowserRouter
    ├── Home
    │   ├── Header
    │   ├── FoodOption
    │   │   └── FoodCard (multiple)
    │   ├── GroceryOption
    │   │   └── GroceryCard (multiple)
    │   └── DineOption
    │       └── DineCard (multiple)
    ├── SecondaryHome
    │   ├── RestHeader
    │   └── Outlet
    │       ├── Restaurant
    │       │   ├── Shimmer (loading)
    │       │   └── RestCard (multiple)
    │       ├── RestaurantMenu
    │       │   └── MenuCard (multiple)
    │       │       └── RestInfo (multiple)
    │       └── SearchFood
    └── Checkout
```

### Data Flow

1. **Restaurant Listing**: `Restaurant.js` fetches data from Swiggy API → Displays in `RestCard` components
2. **Menu Display**: `RestaurantMenu.js` fetches menu by restaurant ID → Renders `MenuCard` → Shows `RestInfo` items
3. **Cart Management**: User clicks ADD → Dispatches Redux action → Updates global cart state → Reflects in `RestHeader`
4. **Checkout**: `Checkout.js` reads cart items from Redux store → Displays selected items

## 🧩 Components Overview

### Page Components
- **Home**: Landing page with all service options
- **Restaurant**: Lists all available restaurants with shimmer loading
- **RestaurantMenu**: Displays menu with veg/non-veg filters
- **SearchFood**: Search interface for menu items
- **Checkout**: Shopping cart with selected items
- **SecondaryHome**: Layout wrapper for restaurant pages

### UI Components
- **Header**: Main navigation header with search bars
- **RestHeader**: Simple header with cart counter
- **RestCard**: Restaurant card with image, name, rating, delivery time
- **MenuCard**: Collapsible menu category with items
- **RestInfo**: Individual menu item with add-to-cart functionality
- **FoodCard/GroceryCard/DineCard**: Category and service cards
- **Shimmer**: Loading skeleton for better UX

## 🔄 State Management

### Redux Store Structure

```javascript
{
  cartslice: {
    items: [
      {
        id: "123",
        name: "Tandoori Paneer",
        quantity: 2,
        price: 250,
        // ... other item details
      }
    ],
    count: 2  // Total number of items
  }
}
```

### Redux Actions

- **addItems**: Adds new item to cart with quantity 1
- **IncrementItems**: Increases item quantity by 1
- **DecrementItems**: Decreases quantity by 1 (removes if quantity becomes 0)

### Usage Example

```javascript
import { useDispatch, useSelector } from 'react-redux';
import { addItems, IncrementItems, DecrementItems } from '../Stored/CartSlicer';

// Get cart data
const items = useSelector(state => state.cartslice.items);
const count = useSelector(state => state.cartslice.count);

// Dispatch actions
const dispatch = useDispatch();
dispatch(addItems(itemData));
dispatch(IncrementItems(itemData));
dispatch(DecrementItems(itemData));
```

## 🌐 API Integration

### Swiggy API Endpoints

**Restaurant List**
```
GET https://www.swiggy.com/dapi/restaurants/list/v5
?lat=28.7040592
&lng=77.10249019999999
&is-seo-homepage-enabled=true
```

**Restaurant Menu**
```
GET https://www.swiggy.com/mapi/menu/pl
?page-type=REGULAR_MENU
&complete-menu=true
&lat=28.7040592
&lng=77.10249019999999
&restaurantId={id}
```

### CORS Proxy
Due to CORS restrictions, the app uses a proxy server:
```javascript
const proxyServer = "https://cors-anywhere.herokuapp.com/";
const response = await fetch(proxyServer + swiggyAPI);
```

**Note**: You may need to request temporary access at https://cors-anywhere.herokuapp.com/corsdemo before using the app.

## 🎨 Styling

The application uses Tailwind CSS for styling with a focus on:
- **Responsive Design**: Mobile-first approach with breakpoints
- **Utility Classes**: Fast development with utility-first CSS
- **Custom Colors**: Orange theme (#ff5200) matching Swiggy branding
- **Animations**: Hover effects and smooth transitions
- **Grid Layouts**: Flexible grids for card displays
- **Overflow Handling**: Horizontal scrolling for category sections

## 📝 Code Documentation

All components include JSDoc documentation with:
- Component description
- Props documentation with types
- Return value description
- Usage examples where applicable

Example:
```javascript
/**
 * RestCard Component
 * Displays a restaurant card with image, name, rating, and delivery time.
 * 
 * @component
 * @param {Object} props - Component props
 * @param {Object} props.restInfo - Restaurant information object
 * @returns {JSX.Element} Restaurant card with hover effect
 */
export default function RestCard({restInfo}) {
  // Component logic
}
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 🐛 Known Issues

1. CORS proxy may require periodic access requests
2. API endpoints are hardcoded for Delhi location
3. Search functionality fetches all data but filtering not fully implemented

## 🚀 Future Enhancements

- [ ] Implement actual search filtering
- [ ] Add user authentication
- [ ] Implement order placement
- [ ] Add payment gateway integration
- [ ] Create user profile and order history
- [ ] Add location detection and selection
- [ ] Implement real-time order tracking
- [ ] Add restaurant reviews and ratings
- [ ] Create admin dashboard
- [ ] Add unit and integration tests

## 📄 License

This project is for educational purposes only.

## 👨‍💻 Author

Built with ❤️ using React, Redux, and Tailwind CSS

---

**Note**: This is a learning project inspired by Swiggy. It uses Swiggy's public API for educational purposes only.
