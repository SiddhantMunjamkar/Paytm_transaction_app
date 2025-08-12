# PayTM Transaction App

A comprehensive digital wallet application built with modern web technologies, featuring user authentication, balance management, peer-to-peer transfers, and banking integrations. This monorepo contains multiple applications and shared packages for a complete financial transaction ecosystem.

## 🏗️ Project Architecture

This project is built as a **Turborepo monorepo** with the following structure:

### Apps
- **`user-app`** - Next.js customer-facing application (Port: 3001)
- **`merchant-app`** - Next.js merchant dashboard application (Port: 3000)
- **`bank-webhook`** - Express.js webhook server for bank integrations (Port: 3003)

### Packages
- **`db`** - Prisma database configuration and client
- **`ui`** - Shared React component library
- **`store`** - Recoil state management atoms and hooks
- **`eslint-config`** - Shared ESLint configurations
- **`typescript-config`** - Shared TypeScript configurations

## 🚀 Features

### User App Features
- **Authentication**: Phone number and password-based login using NextAuth.js
- **Dashboard**: User overview with balance and transaction history
- **Add Money**: On-ramp transactions with bank integrations
- **P2P Transfers**: Send money to other users instantly
- **Transaction History**: View all incoming and outgoing transactions
- **Balance Management**: Real-time balance updates with locked/unlocked amounts

### Merchant App Features
- **Google OAuth**: Merchant authentication via Google
- **Dashboard**: Merchant-specific interface
- **User Management**: Integration with user database

### Bank Webhook
- **Bank Integration**: Webhook endpoint for bank transaction confirmations
- **Transaction Processing**: Secure transaction status updates
- **Balance Updates**: Automatic balance increments on successful payments

## 🛠️ Technology Stack

### Frontend
- **Next.js 14** - React framework with App Router
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first CSS framework
- **NextAuth.js** - Authentication library
- **Recoil** - State management

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework for webhooks
- **Prisma** - Database ORM and migration tool
- **PostgreSQL** - Primary database
- **bcrypt** - Password hashing

### DevOps & Tooling
- **Turborepo** - Monorepo build system
- **ESLint** - Code linting
- **Prettier** - Code formatting
- **TypeScript** - Static type checking

## 📊 Database Schema

### Core Models
- **User**: User accounts with authentication details
- **Balance**: User wallet balances (locked/unlocked)
- **OnRampTransaction**: Bank deposit transactions
- **p2pTransfer**: Peer-to-peer money transfers
- **Merchant**: Merchant account information

### Key Relationships
- Users have one Balance record
- Users can have multiple OnRampTransactions
- Users can send/receive multiple p2pTransfers
- All transactions are properly tracked and auditable

## 🔧 Getting Started

### Prerequisites
- **Node.js** >= 18
- **npm** >= 10.2.4
- **PostgreSQL** database
- **Git**

### 1. Clone the Repository

```bash
git clone <repo-url>
cd Paytm_transaction_app
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Set up PostgreSQL Database

#### Option A: Local PostgreSQL with Docker
```bash
docker run -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:5432 postgres
```

#### Option B: Cloud Database (Recommended)
Use cloud providers like [Neon.tech](https://neon.tech), [Supabase](https://supabase.io), or [Railway](https://railway.app)

### 4. Configure Environment Variables

Create `.env` files in the following directories by copying from `.env.example`:

#### `packages/db/.env`
```env
DATABASE_URL="postgresql://postgres:mysecretpassword@localhost:5432/postgres"
```

#### `apps/user-app/.env`
```env
JWT_SECRET=your-jwt-secret-key
NEXTAUTH_URL=http://localhost:3001
NEXTAUTH_SECRET=your-nextauth-secret
```

#### `apps/merchant-app/.env`
```env
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
NEXTAUTH_SECRET=your-nextauth-secret
```

### 5. Database Setup

Navigate to the database package and set up the database:

```bash
cd packages/db
npx prisma migrate dev
npx prisma db seed
```

This will:
- Apply all database migrations
- Seed the database with test users

### 6. Start Development Servers

#### Start All Applications (Recommended)
```bash
npm run dev
```

#### Or Start Individual Applications
```bash
# User App (Port 3001)
cd apps/user-app && npm run dev

# Merchant App (Port 3000)
cd apps/merchant-app && npm run dev

# Bank Webhook (Port 3003)
cd apps/bank-webhook && npm run dev
```

### 7. Access Applications

- **User App**: http://localhost:3001
- **Merchant App**: http://localhost:3000
- **Bank Webhook**: http://localhost:3003

### 8. Test Login Credentials

The seeded database includes test users:

| Phone Number | Password | Name  | Initial Balance |
|-------------|----------|-------|----------------|
| 1111111111  | alice    | Alice | ₹200.00        |
| 2222222222  | bob      | Bob   | ₹20.00         |

## 📁 Project Structure

```
Paytm_transaction_app/
├── apps/
│   ├── user-app/           # Main user application
│   │   ├── app/           # Next.js app directory
│   │   │   ├── (dashboard)/
│   │   │   │   ├── dashboard/
│   │   │   │   ├── transfer/
│   │   │   │   ├── transactions/
│   │   │   │   └── p2ptransfer/
│   │   │   ├── api/auth/
│   │   │   └── lib/
│   │   └── components/     # React components
│   ├── merchant-app/       # Merchant dashboard
│   │   ├── app/
│   │   ├── lib/
│   │   └── ...
│   └── bank-webhook/       # Webhook server
│       └── src/
├── packages/
│   ├── db/                # Database package
│   │   ├── prisma/
│   │   │   ├── schema.prisma
│   │   │   ├── migrations/
│   │   │   └── seed.ts
│   │   └── index.ts
│   ├── ui/                # Shared components
│   │   └── src/
│   ├── store/             # State management
│   │   └── src/
│   ├── eslint-config/     # ESLint configs
│   └── typescript-config/ # TypeScript configs
└── turbo.json            # Turborepo configuration
```

## 🔄 Available Scripts

### Root Level Commands
```bash
npm run dev      # Start all applications in development mode
npm run build    # Build all applications
npm run lint     # Lint all packages
npm run format   # Format code with Prettier
```

### Application-Specific Commands
```bash
# User App
cd apps/user-app
npm run dev      # Start development server
npm run build    # Build for production
npm run start    # Start production server

# Bank Webhook
cd apps/bank-webhook
npm run dev      # Build and start development server
npm run build    # Build application
npm run start    # Start production server
```

### Database Commands
```bash
cd packages/db
npx prisma migrate dev     # Apply migrations
npx prisma db seed        # Seed database
npx prisma studio         # Open Prisma Studio
npx prisma generate       # Generate Prisma client
```

## 🔐 Security Features

- **Password Hashing**: bcrypt for secure password storage
- **JWT Authentication**: Secure session management
- **Database Transactions**: Atomic operations for financial transactions
- **Row-level Locking**: Prevents race conditions in balance updates
- **Input Validation**: Type-safe operations with TypeScript
- **Environment Variables**: Sensitive data stored securely

## 🚦 API Endpoints

### User App APIs
- `GET /api/user` - Get current user information
- `POST /api/auth/signin` - User authentication
- `POST /api/auth/signout` - User logout

### Bank Webhook APIs
- `POST /bankWebhook` - Bank webhook for transaction confirmations

## 🧪 Testing

### Test Users
The application comes with pre-seeded test users for development:

- **Alice** (1111111111): Primary test user with ₹200 balance
- **Bob** (2222222222): Secondary test user with ₹20 balance

### Testing Scenarios
1. **Login Flow**: Use provided credentials to test authentication
2. **Add Money**: Test on-ramp transactions (redirects to bank simulation)
3. **P2P Transfer**: Send money between test users
4. **Balance Updates**: Verify real-time balance changes
5. **Transaction History**: Check transaction logs

## 🏦 Bank Integration

### Bank Integration
- **Webhook Endpoint**: `/bankWebhook`
- **Supported Operations**: Deposit confirmations
- **Security**: Token-based transaction verification

### Adding New Banks
1. Add bank configuration in `AddMoneyCard.tsx`
2. Create new webhook endpoint in `bank-webhook`
3. Update database schema if needed

## 🔧 Development Guidelines

### Adding New Features
1. **UI Components**: Add to `packages/ui/src/`
2. **State Management**: Add atoms to `packages/store/src/atoms/`
3. **Database Changes**: Create new migrations in `packages/db/prisma/migrations/`
4. **API Routes**: Add to respective app's `api/` directory

### Code Style
- Follow ESLint configuration
- Use TypeScript for type safety
- Follow component naming conventions
- Add proper error handling

## 🚀 Deployment

### Environment Setup
1. Set up production PostgreSQL database
2. Configure environment variables for production
3. Set up proper secrets management

### Build Commands
```bash
npm run build    # Build all applications
```

### Deployment Platforms
- **Vercel**: Recommended for Next.js applications
- **Railway**: Good for full-stack deployment
- **Docker**: Containerized deployment option

## 📝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 🐛 Troubleshooting

### Common Issues

1. **Database Connection**: Ensure PostgreSQL is running and connection string is correct
2. **Port Conflicts**: Check if ports 3000, 3001, 3003 are available
3. **Environment Variables**: Verify all required `.env` files are configured
4. **Node Version**: Ensure Node.js >= 18 is installed

### Useful Commands
```bash
# Reset database
cd packages/db && npx prisma migrate reset

# View database
cd packages/db && npx prisma studio

# Clear node modules
rm -rf node_modules && npm install

# Check running processes
lsof -i :3001  # Check what's running on port 3001
```

## 🤝 Support

For support and questions:
1. Check the troubleshooting section
2. Review the codebase documentation
3. Create an issue in the repository

---

**Happy Coding! 💻✨**
