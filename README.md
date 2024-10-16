import React from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import ChristmasList from './components/ChristmasList';
import FestiveLayout from './components/FestiveLayout';
import Messages from './components/Messages';

function App() {
  return (
    <FestiveLayout>
      <Router>
        <Switch>
          <Route path="/list" component={ChristmasList} />
          <Route path="/messages" component={Messages} />
        </Switch>
      </Router>
    </FestiveLayout>
  );
}

export default App;
import React, { useState } from 'react';

const ChristmasList = () => {
  const [items, setItems] = useState([{ id: 1, name: "New Bike", purchased: false }]);
  const [newItem, setNewItem] = useState('');

  const addItem = () => {
    setItems([...items, { id: items.length + 1, name: newItem, purchased: false }]);
    setNewItem('');
  };

  const markAsPurchased = (id) => {
    setItems(items.map(item => 
      item.id === id ? { ...item, purchased: true } : item
    ));
  };

  return (
    <div className="list-container">
      <h2>Christmas List</h2>
      <ul>
        {items.map(item => (
          <li key={item.id}>
            {item.name} 
            {!item.purchased && (
              <button onClick={() => markAsPurchased(item.id)}>Mark as Purchased</button>
            )}
          </li>
        ))}
      </ul>
      <input 
        value={newItem} 
        onChange={(e) => setNewItem(e.target.value)} 
        placeholder="Add a new item" 
      />
      <button onClick={addItem}>Add Item</button>
    </div>
  );
};

export default ChristmasList;
import React, { useState } from 'react';

const Messages = ({ excludedUser }) => {
  const [messages, setMessages] = useState([]);
  const [newMessage, setNewMessage] = useState('');

  const sendMessage = () => {
    if (excludedUser) {
      setMessages([...messages, { text: newMessage, toAllExcept: excludedUser }]);
    } else {
      setMessages([...messages, { text: newMessage, toAllExcept: null }]);
    }
    setNewMessage('');
  };

  return (
    <div className="messages-container">
      <h2>Group Messages (Excluding {excludedUser})</h2>
      <ul>
        {messages.map((msg, index) => (
          <li key={index}>
            {msg.text} {msg.toAllExcept && `(Hidden from ${msg.toAllExcept})`}
          </li>
        ))}
      </ul>
      <input 
        value={newMessage} 
        onChange={(e) => setNewMessage(e.target.value)} 
        placeholder="Type your message" 
      />
      <button onClick={sendMessage}>Send Message</button>
    </div>
  );
};

export default Messages;
import React from 'react';
import './FestiveLayout.css';  // Add this CSS for the theming

const FestiveLayout = ({ children }) => {
  return (
    <div className="festive-layout">
      <header className="header">
        <h1>🎄 Christmas Gift List 🎄</h1>
      </header>
      <main>
        {children}
      </main>
      <footer className="footer">
        <p>Happy Holidays! 🎁</p>
      </footer>
    </div>
  );
};

export default FestiveLayout;
body {
  background: url('https://path-to-snowy-background-image.jpg') no-repeat center center fixed;
  background-size: cover;
  font-family: 'Merienda', cursive; /* You can load a festive Google Font */
}

.festive-layout {
  text-align: center;
  color: white;
}

.header {
  background-color: #4CAF50;  /* Christmas green */
  padding: 20px;
  box-shadow: 0 4px 2px -2px gray;
}

.footer {
  background-color: #D32F2F;  /* Christmas red */
  padding: 10px;
  position: fixed;
  width: 100%;
  bottom: 0;
}

.list-container, .messages-container {
  background-color: rgba(255, 255, 255, 0.8);
  margin: 20px;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

button {
  background-color: #F44336;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #E53935;
}
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
