#  AI-Powered Tire Chatbot & E-Commerce Platform

A full-stack application that combines AI-powered customer support with e-commerce functionality for tire shopping. Users can interact with an intelligent chatbot, discover tires through natural language queries, and complete purchases with Stripe integration.

**Built with:** React • Express.js • OpenAI • Stripe • Tailwind CSS • Web Speech API

---

## Key Features

###  AI-Powered Conversational Chatbot
- **OpenAI Integration**: Intelligent responses to tire-related queries with context awareness
- **Smart Tire Matching**: Recognizes tire brands, models, and specifications
- **Natural Language Processing**: Understands queries like:
  - "Do you have Michelin Pilot Sport 4?"
  - "Tires for Honda Civic 2018"
  - "Tires with size 275/65R18"
  - "Best tires for winter driving"

###  Voice-Enabled Interaction
- **Web Speech API**: Real-time speech-to-text conversion
- **Hands-free Experience**: Speak queries instead of typing
- **Browser Compatible**: Works on Chrome, Firefox, Safari, and Edge

###  Secure Payment Processing
- **Stripe Payment Gateway**: PCI-compliant card processing
- **Webhook Support**: Real-time order confirmation on successful payment
- **Order Management**: Tracks customer orders and payment status

### Responsive Frontend
- **Modern UI**: Built with React and Tailwind CSS
- **Component-Based Architecture**: Reusable, maintainable components
- **Smooth Navigation**: React Router for seamless page transitions
- **Mobile-First Design**: Works on desktop, tablet, and mobile

###  Express Backend API
- **RESTful Routes**: Well-structured API endpoints
- **Middleware**: CORS, body parsing, request logging
- **Dataset Management**: JSON-based tire inventory system
- **Webhook Handling**: Stripe event processing for payment confirmations

---

## 📁 Project Structure

```
Chat_Assistant_For_Tires/
├── frontend/                    # React frontend application
│   ├── public/
│   │   ├── index.html          # Main HTML entry point
│   │   ├── manifest.json       # PWA manifest
│   │   └── robots.txt
│   ├── src/
│   │   ├── App.js              # Main app with routing
│   │   ├── index.js            # React entry point
│   │   ├── index.css           # Global styles
│   │   ├── components/
│   │   │   └── Chatbot.jsx     # Main chatbot component
│   │   └── pages/
│   │       ├── OrderForm.jsx   # Order form page
│   │       ├── Success.jsx     # Payment success page
│   │       └── hi.js
│   ├── package.json            # Frontend dependencies
│   ├── tailwind.config.js      # Tailwind CSS configuration
│   └── postcss.config.js       # PostCSS configuration
│
├── backend/                     # Express backend server
│   ├── server.js               # Main server file
│   ├── package.json            # Backend dependencies
│   ├── dataset.json            # Tire inventory data
│   ├── tires.json              # Additional tire data
│   ├── tireImages.json         # Tire image mappings
│   ├── Sucess.jsx              # Success component (copy)
│   └── routes/
│       ├── chat.js             # ChatGPT integration & tire matching
│       ├── order.js            # Order management endpoints
│       └── stripe.js           # Stripe payment session creation
│
├── LICENSE                      # MIT License
└── README.md                    # This file
```

---

## Getting Started

### Prerequisites
- **Node.js** (v14+) and npm/yarn
- **OpenAI API Key** ([Get it here](https://platform.openai.com/api-keys))
- **Stripe Account** ([Sign up here](https://stripe.com))

### Backend Setup

1. **Navigate to backend folder**
   ```bash
   cd backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Create `.env` file** in the `backend` directory
   ```env
   OPENAI_API_KEY=your_openai_api_key_here
   STRIPE_SECRET_KEY=your_stripe_secret_key_here
   STRIPE_PUBLISHABLE_KEY=your_stripe_publishable_key_here
   STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret_here
   PORT=3001
   ```

4. **Start the server**
   ```bash
   npm start          # Production mode
   npm run dev        # Development mode with nodemon
   ```

   Server runs on `http://localhost:3001`

### Frontend Setup

1. **Navigate to frontend folder** (in a new terminal)
   ```bash
   cd frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Create `.env` file** in the `frontend` directory
   ```env
   REACT_APP_API_URL=http://localhost:3001
   REACT_APP_STRIPE_PUBLIC_KEY=your_stripe_publishable_key_here
   ```

4. **Start the development server**
   ```bash
   npm start
   ```

   Frontend runs on `http://localhost:3000`

---

## 📡 API Endpoints

### Chat Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/chatbot` | Send message to chatbot, get AI response |
| GET | `/api/chatbot/ping` | Health check for chatbot service |

**Request Body Example:**
```json
{
  "messages": [
    {
      "role": "user",
      "content": "Do you have Michelin Pilot Sport 4?"
    }
  ]
}
```

### Order Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/order/place` | Create a new order |
| GET | `/api/order/all` | Get all orders |

**Request Body Example:**
```json
{
  "customerName": "John Doe",
  "address": "123 Main St, City, State 12345",
  "phone": "555-123-4567",
  "tireId": "michelin_pilot_sport_4",
  "quantity": 4
}
```

### Payment Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/stripe/create-checkout-session` | Initialize Stripe checkout |
| POST | `/api/webhook` | Stripe webhook for payment events |

**Request Body Example:**
```json
{
  "customerName": "John Doe",
  "address": "123 Main St, City, State 12345",
  "phone": "555-123-4567",
  "tireName": "Michelin Pilot Sport 4",
  "quantity": 4,
  "totalAmount": 800
}
```

---

## 🛠️ Technology Stack

### Frontend
- **React 19** - UI library
- **React Router DOM 7** - Client-side routing
- **Tailwind CSS** - Utility-first CSS framework
- **Axios** - HTTP client
- **Stripe React** - Payment integration
- **React Icons** - Icon library
- **Web Speech API** - Voice recognition (native browser)

### Backend
- **Express.js** - Web framework
- **OpenAI API** - AI-powered responses
- **Stripe** - Payment processing
- **CORS** - Cross-origin resource sharing
- **Dotenv** - Environment variable management
- **Nodemon** - Development auto-reload

### Data
- **JSON-based Dataset** - Tire inventory stored in JSON files
- **In-Memory Storage** - Orders (upgrade to database for production)

---

## 🔄 Data Flow

### User Query to Tire Match
```
1. User sends message via chat UI
2. Frontend sends to /api/chatbot endpoint
3. Backend checks if query mentions tire brand/model
4. If matched: Returns matching tires from dataset.json
5. If no match: Forwards to OpenAI for intelligent response
6. Response displayed in chat with tire cards (if applicable)
```

### Order Placement with Payment
```
1. User clicks "Buy Now" or completes order form
2. Frontend creates Stripe checkout session via /api/stripe/create-checkout-session
3. Stripe hosted checkout page opens
4. Customer enters card details and confirms payment
5. Stripe sends webhook to /api/webhook
6. Backend saves order with "Paid" status
7. User redirected to success page
```

---

## 📊 Dataset Structure

### `dataset.json` Format
```json
[
  {
    "id": "1",
    "brand": "Michelin",
    "model": "Pilot Sport 4",
    "size": "275/65R18",
    "price": 250,
    "rating": 4.8,
    "stock": 50,
    "image_url": "url_to_image",
    "product_url": "url_to_product"
  }
]
```

---

## 🔐 Security Considerations

- **API Keys**: Store in `.env` files (never commit to version control)
- **Stripe Webhooks**: Verify webhook signatures using `process.env.STRIPE_WEBHOOK_SECRET`
- **CORS**: Configure to allow only trusted origins
- **Input Validation**: Validate all user inputs on both frontend and backend
- **HTTPS**: Use HTTPS in production
- **Rate Limiting**: Consider adding rate limiting for API endpoints

---

## 🐛 Troubleshooting

### Common Issues

**"CORS policy: No 'Access-Control-Allow-Origin'"**
- Ensure backend is running on port 3001
- Check CORS configuration in `server.js`

**"OpenAI API key not found"**
- Verify `.env` file exists in backend folder
- Check `OPENAI_API_KEY` is correctly set

**"Stripe webhook fails"**
- Ensure webhook secret is correct in `.env`
- Check webhook is forwarding to correct endpoint
- Review Stripe dashboard for webhook logs

**"Speech recognition not working"**
- Only works on HTTPS or localhost
- Supported on Chrome, Firefox, Safari, Edge
- Check browser microphone permissions

---

##  To-Do / Future Enhancements

- [ ] Replace in-memory order storage with database (MongoDB/PostgreSQL)
- [ ] Add user authentication and order history
- [ ] Implement email notifications for order confirmation
- [ ] Add real-time order tracking
- [ ] Integrate more tire data sources
- [ ] Add tire comparison feature
- [ ] Implement advanced search filters
- [ ] Add customer reviews and ratings
- [ ] Mobile app version
- [ ] Multi-language support

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**NaveenKancharla28**

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
│ ├── order.js # In-memory order storage
│ └── dataset.json # Tire listings
└── .env # OpenAI + Stripe keys (not committed)

yaml
Copy
Edit
