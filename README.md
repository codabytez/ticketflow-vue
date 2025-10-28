# TicketFlow Vue - Ticket Management System

A modern, responsive ticket management web application built with Vue.js 3, Vite, and Tailwind CSS.

## 🚀 Features

### Core Functionality

- **Landing Page**: Beautiful hero section with wavy SVG background and decorative elements
- **Authentication**: Secure login and signup with validation and session management
- **Dashboard**: Overview with ticket statistics and quick actions
- **Ticket Management**: Full CRUD operations (Create, Read, Update, Delete)

### Technical Features

- ✅ Vue 3 Composition API with `<script setup>`
- ✅ Tailwind CSS for styling
- ✅ Responsive design (mobile, tablet, desktop)
- ✅ Form validation with inline error messages
- ✅ Toast notifications for user feedback
- ✅ LocalStorage for data persistence
- ✅ Protected routes with authentication
- ✅ Smooth transitions and animations

## 📋 Requirements Met

- **Max-width**: 1440px centered layout on all pages
- **Wave Background**: SVG wave in hero section
- **Decorative Circles**: Multiple circular blur elements
- **Status Colors**:
  - Open → Green (`bg-green-500`)
  - In Progress → Amber (`bg-amber-500`)
  - Closed → Gray (`bg-gray-500`)
- **Authentication**: Session stored as `ticketapp_session` in localStorage
- **Validation**: Title and status fields are mandatory
- **Error Handling**: Consistent error messages and toast notifications

## 🛠️ Tech Stack

- **Framework**: Vue.js 3.3.4
- **Build Tool**: Vite 4.4.9
- **Styling**: Tailwind CSS 3.3.3
- **JavaScript**: ES6+

## 📦 Installation

1. **Clone or download the repository**

1. **Navigate to the Vue project directory**

```bash
cd ticketflow-vue
```

1. **Install dependencies**

```bash
pnpm install
```

1. **Start the development server**

```bash
pnpm dev
```

1. **Open your browser**
   Navigate to `http://localhost:3001`

## 🏗️ Project Structure

```Vue
ticketflow-vue/
├── public/
├── src/
│   ├── App.vue          # Main application component
│   ├── main.ts          # Application entry point
│   └── style.css        # Global styles with Tailwind
├── index.html           # HTML template
├── package.json         # Dependencies and scripts
├── vite.config.js       # Vite configuration
└── README.md           # This file
```

## 🎨 Design System

### Colors

- **Primary**: Indigo (`#4F46E5`)
- **Success**: Green (`#10B981`)
- **Warning**: Amber (`#F59E0B`)
- **Danger**: Red (`#EF4444`)
- **Gray**: Various shades for text and backgrounds

### Typography

- **Headings**: Bold, large sizes for hierarchy
- **Body**: Regular weight, readable sizes
- **Labels**: Medium weight, smaller sizes

### Spacing

- Consistent padding and margins using Tailwind's spacing scale
- Card-based layout with rounded corners and shadows

## 🔐 Auth

### Session Management

- Sessions are stored in `localStorage` with the key `ticketapp_session`
- Token format: Base64 encoded `email:timestamp`
- Protected routes redirect to login if no valid session exists

### Test Credentials

You can use any email and password combination:

- **Email**: Any valid email format (e.g., `test@example.com`)
- **Password**: Minimum 6 characters

## 📝 Ticket Structure

```javascript
{
  id: string,              // Unique identifier (timestamp)
  title: string,           // Required
  description: string,     // Optional
  status: 'open' | 'in_progress' | 'closed',  // Required
  priority: 'low' | 'medium' | 'high',        // Optional
  createdAt: string       // ISO timestamp
}
```

## ✨ Key Components

### Landing Page

- Hero section with gradient background
- Decorative circular elements
- Wavy SVG divider
- Feature cards
- Footer

### Authentication

- Email and password validation
- Inline error messages
- Toast notifications
- Switch between login/signup

### Dashboard

- Ticket statistics cards
- Color-coded status indicators
- Quick action buttons
- Logout functionality

### Ticket Management

- Create new tickets
- Edit existing tickets
- Delete with confirmation
- List view with cards
- Status badges
- Form validation

## 🎯 Validation Rules

### Email Validation

- **Email**: Must be valid email format
- **Password**: Minimum 6 characters

### Tickets

- **Title**: Required, cannot be empty
- **Status**: Must be one of: `open`, `in_progress`, `closed`
- **Description**: Optional, no validation
- **Priority**: Optional, defaults to `medium`

## 🚨 Error Handling

The application handles errors in multiple ways:

1. **Inline Validation**: Displayed beneath form fields
2. **Toast Notifications**: Shown for actions and errors
3. **Route Protection**: Redirects to login for unauthorized access
4. **Confirmation Dialogs**: For destructive actions (delete)

## 📱 Responsive Breakpoints

- **Mobile**: < 640px (sm)
- **Tablet**: 640px - 1024px (md)
- **Desktop**: > 1024px (lg)

## 🔧 Build Commands

```bash
# Install dependencies
pnpm install

# Run development server
pnpm dev

# Build for production
pnpm build

# Preview production build
pnpm preview
```

## Author

### Lisan al Gaib

- GitHub: [@codabytez](https://github.com/codabytez)
- Twitter: [@codabytez](https://x.com/codabytez)
- LinkedIn: [Lisan al Gaib](https://www.linkedin.com/in/codabytez)

## 🙏 Acknowledgments

- Built for HNG Internship Frontend Track Stage 2
- Design inspiration from behance
