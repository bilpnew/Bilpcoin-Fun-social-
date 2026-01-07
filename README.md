import React, { useState, useEffect, useRef } from 'react';
import { RotateCcw, Play, Pause, SkipForward, Users, Award, Zap, Dice5, Puzzle, Target, Gamepad2, Circle, Square, Triangle, Star, Music, Hash, MessageSquare, Send, Heart, RefreshCw, User, TrendingUp, Share2, Twitter, Facebook, Instagram, Linkedin, Copy, Check, Sun, Moon, TrendingDown, DollarSign, ChartLine, BarChart3, Network, Users2, Bitcoin, ArrowUpRight, ArrowDownRight, Plus, Minus, HashIcon, AtSign, Link, Image as ImageIcon, Calendar, MapPin, Briefcase, GraduationCap, Palette, Camera, Bell, Search, MoreHorizontal } from 'lucide-react';

// Bilpcoin Social Component (Enhanced Twitter Clone)
const BilpcoinSocial = ({ isActive, isDarkMode }) => {
  const [posts, setPosts] = useState([]);
  const [newPost, setNewPost] = useState('');
  const [newPostImage, setNewPostImage] = useState(null);
  const [user, setUser] = useState({
    name: 'Bilpcoin User',
    username: '@bilpcoin_user',
    bio: 'Gaming enthusiast and crypto trader 🎮💰',
    location: 'Crypto Valley',
    website: 'bilpcoin.fun',
    joinDate: 'January 2024',
    following: 245,
    followers: 189,
    avatar: '👤'
  });
  
  const [currentUser, setCurrentUser] = useState({
    name: 'You',
    username: '@you',
    avatar: '🥸'
  });
  
  const [trending, setTrending] = useState([
    { topic: '#Bilpcoin', tweets: '12.5K' },
    { topic: '#CryptoGaming', tweets: '8.2K' },
    { topic: '#TradingWin', tweets: '5.7K' },
    { topic: '#GameDevelopment', tweets: '3.1K' },
    { topic: '#NFTGaming', tweets: '2.8K' }
  ]);
  
  const [suggestions, setSuggestions] = useState([
    { name: 'CryptoGamer', username: '@crypto_gamer', avatar: '🎮', following: true },
    { name: 'TradingPro', username: '@trading_pro', avatar: '📈', following: false },
    { name: 'GameDev', username: '@game_dev', avatar: '💻', following: false },
    { name: 'NFTCollector', username: '@nft_collector', avatar: '🎨', following: true }
  ]);
  
  const [likes, setLikes] = useState({});
  const [comments, setComments] = useState({});
  const [bookmarks, setBookmarks] = useState({});
  const [showImagePreview, setShowImagePreview] = useState(false);
  const fileInputRef = useRef(null);
  const messagesEndRef = useRef(null);

  // Mock data for initial posts
  useEffect(() => {
    if (isActive) {
      const initialPosts = [
        {
          id: 1,
          content: "Just made $2,500 in the Crypto Trading Simulator! 🚀 The leverage feature is incredible. #BilpcoinTrading #WinBig",
          timestamp: "2 hours ago",
          likes: 45,
          comments: 12,
          bookmarks: 8,
          user: { name: "CryptoGamer", username: "@crypto_gamer", avatar: "🎮" },
          image: null
        },
        {
          id: 2,
          content: "Won 5 games in a row on the Card Challenge! My secret strategy involves always playing high cards first. What's your strategy? 🃏",
          timestamp: "4 hours ago",
          likes: 32,
          comments: 18,
          bookmarks: 5,
          user: { name: "CardMaster", username: "@card_master", avatar: "🃏" },
          image: "https://placehold.co/400x200/6366f1/white?text=Card+Game+Screenshot"
        },
        {
          id: 3,
          content: "The new Multiplayer Poker room is absolutely fire! Just beat 3 other players in a high-stakes tournament. 💸 #PokerNight #BilpcoinFun",
          timestamp: "6 hours ago",
          likes: 67,
          comments: 23,
          bookmarks: 15,
          user: { name: "PokerKing", username: "@poker_king", avatar: "👑" },
          image: null
        },
        {
          id: 4,
          content: "Stock Market Simulator update is live! Now you can trade real-time with margin trading. Made 15% ROI in just one day! 📊",
          timestamp: "8 hours ago",
          likes: 89,
          comments: 31,
          bookmarks: 22,
          user: { name: "StockGuru", username: "@stock_guru", avatar: "📊" },
          image: "https://placehold.co/400x200/10b981/white?text=Stock+Chart+Screenshot"
        }
      ];
      setPosts(initialPosts);
    }
  }, [isActive]);

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!newPost.trim()) return;
    
    const post = {
      id: Date.now(),
      content: newPost,
      timestamp: "Just now",
      likes: 0,
      comments: 0,
      bookmarks: 0,
      user: currentUser,
      image: newPostImage
    };
    
    setPosts(prev => [post, ...prev]);
    setNewPost('');
    setNewPostImage(null);
    setShowImagePreview(false);
  };

  const handleLike = (postId) => {
    setLikes(prev => ({
      ...prev,
      [postId]: !prev[postId]
    }));
  };

  const handleComment = (postId) => {
    const commentCount = comments[postId] || 0;
    setComments(prev => ({
      ...prev,
      [postId]: commentCount + 1
    }));
  };

  const handleBookmark = (postId) => {
    setBookmarks(prev => ({
      ...prev,
      [postId]: !prev[postId]
    }));
  };

  const handleImageUpload = (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (event) => {
        setNewPostImage(event.target.result);
        setShowImagePreview(true);
      };
      reader.readAsDataURL(file);
    }
  };

  const removeImage = () => {
    setNewPostImage(null);
    setShowImagePreview(false);
    if (fileInputRef.current) {
      fileInputRef.current.value = '';
    }
  };

  const scrollToBottom = () => {
    messagesEndRef.current?.scrollIntoView({ behavior: "smooth" });
  };

  useEffect(() => {
    scrollToBottom();
  }, [posts]);

  if (!isActive) return null;

  return (
    <div className="max-w-6xl mx-auto">
      {/* Header */}
      <div className={`p-4 rounded-xl mb-6 ${isDarkMode ? 'bg-gradient-to-r from-purple-900 to-indigo-900' : 'bg-gradient-to-r from-purple-200 to-indigo-200'}`}>
        <div className="flex items-center gap-3 mb-4">
          <div className="w-12 h-12 bg-gradient-to-r from-yellow-400 to-orange-500 rounded-full flex items-center justify-center text-2xl">
            ₿
          </div>
          <div>
            <h1 className={`text-2xl font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>Bilpcoin Social</h1>
            <p className={`${isDarkMode ? 'text-purple-200' : 'text-purple-600'}`}>Connect, Share, and Game Together</p>
          </div>
        </div>
        
        <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
          <div className={`p-3 rounded-lg ${isDarkMode ? 'bg-black bg-opacity-30' : 'bg-white bg-opacity-50'}`}>
            <div className="text-center">
              <div className={`text-2xl font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>{posts.length + 245}</div>
              <div className={`${isDarkMode ? 'text-gray-400' : 'text-gray-600'}`}>Total Posts</div>
            </div>
          </div>
          <div className={`p-3 rounded-lg ${isDarkMode ? 'bg-black bg-opacity-30' : 'bg-white bg-opacity-50'}`}>
            <div className="text-center">
              <div className={`text-2xl font-bold ${isDarkMode ? 'text-green-400' : 'text-green-600'}`}>1.2K</div>
              <div className={`${isDarkMode ? 'text-gray-400' : 'text-gray-600'}`}>Active Users</div>
            </div>
          </div>
          <div className={`p-3 rounded-lg ${isDarkMode ? 'bg-black bg-opacity-30' : 'bg-white bg-opacity-50'}`}>
            <div className="text-center">
              <div className={`text-2xl font-bold ${isDarkMode ? 'text-blue-400' : 'text-blue-600'}`}>14</div>
              <div className={`${isDarkMode ? 'text-gray-400' : 'text-gray-600'}`}>Games Available</div>
            </div>
          </div>
        </div>
      </div>

      <div className="grid grid-cols-1 lg:grid-cols-4 gap-6">
        {/* Main Feed */}
        <div className="lg:col-span-2">
          {/* Post Composer */}
          <div className={`p-4 rounded-xl mb-6 ${isDarkMode ? 'bg-black bg-opacity-30' : 'bg-white bg-opacity-70'} backdrop-blur-sm`}>
            <form onSubmit={handleSubmit}>
              <div className="flex gap-3">
                <div className="w-10 h-10 bg-gradient-to-r from-yellow-400 to-orange-500 rounded-full flex items-center justify-center text-white font-bold">
                  {currentUser.avatar}
                </div>
                <div className="flex-1">
                  <textarea
                    value={newPost}
                    onChange={(e) => setNewPost(e.target.value)}
                    placeholder="What's happening in your Bilpcoin Fun journey?"
                    className={`w-full p-3 ${isDarkMode ? 'bg-gray-800 text-white' : 'bg-gray-100 text-gray-800'} rounded-lg mb-3 min-h-20 resize-none`}
                    maxLength={280}
                  />
                  
                  {showImagePreview && newPostImage && (
                    <div className="mb-3 relative">
                      <img 
                        src={newPostImage} 
                        alt="Post preview" 
                        className="w-full h-48 object-cover rounded-lg"
                      />
                      <button
                        onClick={removeImage}
                        className="absolute top-2 right-2 bg-red-500 text-white rounded-full p-1 hover:bg-red-600"
                      >
                        ✕
                      </button>
                    </div>
                  )}
                  
                  <div className="flex justify-between items-center">
                    <div className="flex gap-2">
                      <button
                        type="button"
                        onClick={() => fileInputRef.current?.click()}
                        className={`p-2 rounded-full ${isDarkMode ? 'hover:bg-gray-700' : 'hover:bg-gray-200'}`}
                      >
                        <ImageIcon size={20} className={isDarkMode ? 'text-gray-300' : 'text-gray-600'} />
                      </button>
                      <input
                        type="file"
                        ref={fileInputRef}
                        onChange={handleImageUpload}
                        accept="image/*"
                        className="hidden"
                      />
                      <button
                        type="button"
                        className={`p-2 rounded-full ${isDarkMode ? 'hover:bg-gray-700' : 'hover:bg-gray-200'}`}
                      >
                        <HashIcon size={20} className={isDarkMode ? 'text-gray-300' : 'text-gray-600'} />
                      </button>
                    </div>
                    <div className="flex items-center gap-2">
                      <span className={`${isDarkMode ? 'text-gray-400' : 'text-gray-500'} text-sm`}>{newPost.length}/280</span>
                      <button
                        type="submit"
                        disabled={!newPost.trim()}
                        className="flex items-center gap-2 px-4 py-2 bg-gradient-to-r from-blue-500 to-indigo-600 text-white rounded-full font-bold hover:from-blue-600 hover:to-indigo-700 transform hover:scale-105 transition-all duration-200 disabled:opacity-50"
                      >
                        <Send size={16} />
                        Post
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </form>
          </div>

          {/* Posts Feed */}
          <div className="space-y-4">
            {posts.map((post) => (
              <div key={post.id} className={`rounded-xl p-4 ${isDarkMode ? 'bg-black bg-opacity-20' : 'bg-white bg-opacity-50'} border border-purple-500 border-opacity-20`}>
                <div className="flex gap-3">
                  <div className="w-10 h-10 bg-gradient-to-r from-yellow-400 to-orange-500 rounded-full flex items-center justify-center text-white font-bold">
                    {post.user.avatar}
                  </div>
                  <div className="flex-1">
                    <div className="flex items-center gap-2 mb-2">
                      <span className={`font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>{post.user.name}</span>
                      <span className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>{post.user.username}</span>
                      <span className={isDarkMode ? 'text-gray-500' : 'text-gray-400'}>·</span>
                      <span className={`${isDarkMode ? 'text-gray-500' : 'text-gray-400'} text-sm`}>{post.timestamp}</span>
                    </div>
                    <p className={`${isDarkMode ? 'text-white' : 'text-gray-800'} mb-3 leading-relaxed`}>{post.content}</p>
                    
                    {post.image && (
                      <div className="mb-3 rounded-lg overflow-hidden">
                        <img 
                          src={post.image} 
                          alt="Post content" 
                          className="w-full h-48 object-cover"
                        />
                      </div>
                    )}
                    
                    <div className="flex justify-between pt-3 border-t border-gray-600 border-opacity-30">
                      <button
                        onClick={() => handleComment(post.id)}
                        className={`flex items-center gap-1 ${isDarkMode ? 'text-gray-400 hover:text-blue-400' : 'text-gray-500 hover:text-blue-600'} transition-colors`}
                      >
                        <MessageSquare size={18} />
                        <span>{post.comments + (comments[post.id] || 0)}</span>
                      </button>
                      <button
                        onClick={() => handleBookmark(post.id)}
                        className={`flex items-center gap-1 ${isDarkMode ? 'text-gray-400 hover:text-purple-400' : 'text-gray-500 hover:text-purple-600'} transition-colors`}
                      >
                        <Star size={18} className={`${bookmarks[post.id] ? (isDarkMode ? 'text-purple-400 fill-current' : 'text-purple-600 fill-current') : ''}`} />
                        <span>{post.bookmarks + (bookmarks[post.id] ? 1 : 0)}</span>
                      </button>
                      <button
                        onClick={() => handleLike(post.id)}
                        className={`flex items-center gap-1 ${isDarkMode ? 'text-gray-400 hover:text-red-400' : 'text-gray-500 hover:text-red-600'} transition-colors`}
                      >
                        <Heart size={18} className={`${likes[post.id] ? (isDarkMode ? 'text-red-400 fill-current' : 'text-red-600 fill-current') : ''}`} />
                        <span>{post.likes + (likes[post.id] ? 1 : 0)}</span>
                      </button>
                      <button
                        className={`flex items-center gap-1 ${isDarkMode ? 'text-gray-400 hover:text-green-400' : 'text-gray-500 hover:text-green-600'} transition-colors`}
                      >
                        <Share2 size={18} />
                        <span>Share</span>
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            ))}
            <div ref={messagesEndRef} />
          </div>
        </div>

        {/* Sidebar */}
        <div className="lg:col-span-2 space-y-6">
          {/* User Profile Card */}
          <div className={`p-4 rounded-xl ${isDarkMode ? 'bg-black bg-opacity-30' : 'bg-white bg-opacity-70'} backdrop-blur-sm`}>
            <div className="text-center mb-4">
              <div className="w-16 h-16 bg-gradient-to-r from-yellow-400 to-orange-500 rounded-full flex items-center justify-center text-2xl mx-auto mb-3">
                {user.avatar}
              </div>
              <h3 className={`font-bold text-lg ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>{user.name}</h3>
              <p className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>{user.username}</p>
            </div>
            
            <p className={`text-sm mb-4 text-center ${isDarkMode ? 'text-gray-300' : 'text-gray-600'}`}>{user.bio}</p>
            
            <div className="grid grid-cols-2 gap-4 mb-4">
              <div className="text-center">
                <div className={`font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>{user.following}</div>
                <div className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>Following</div>
              </div>
              <div className="text-center">
                <div className={`font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>{user.followers}</div>
                <div className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>Followers</div>
              </div>
            </div>
            
            <div className={`text-sm space-y-1 ${isDarkMode ? 'text-gray-400' : 'text-gray-500'}`}>
              <div className="flex items-center gap-2">
                <MapPin size={14} />
                <span>{user.location}</span>
              </div>
              <div className="flex items-center gap-2">
                <Link size={14} />
                <span>{user.website}</span>
              </div>
              <div className="flex items-center gap-2">
                <Calendar size={14} />
                <span>Joined {user.joinDate}</span>
              </div>
            </div>
          </div>

          {/* Trending Topics */}
          <div className={`p-4 rounded-xl ${isDarkMode ? 'bg-black bg-opacity-30' : 'bg-white bg-opacity-70'} backdrop-blur-sm`}>
            <h3 className={`text-lg font-bold mb-4 flex items-center gap-2 ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>
              <TrendingUp size={20} className="text-green-500" />
              Trending Now
            </h3>
            <div className="space-y-3">
              {trending.map((trend, index) => (
                <div key={index} className="flex justify-between items-center pb-2 border-b border-gray-600 border-opacity-30">
                  <div>
                    <div className={`font-semibold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>{trend.topic}</div>
                    <div className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>{trend.tweets} posts</div>
                  </div>
                  <MoreHorizontal size={20} className={isDarkMode ? 'text-gray-400' : 'text-gray-500'} />
                </div>
              ))}
            </div>
          </div>

          {/* Who to Follow */}
          <div className={`p-4 rounded-xl ${isDarkMode ? 'bg-black bg-opacity-30' : 'bg-white bg-opacity-70'} backdrop-blur-sm`}>
            <h3 className={`text-lg font-bold mb-4 ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>Who to follow</h3>
            <div className="space-y-3">
              {suggestions.map((suggestion, index) => (
                <div key={index} className="flex items-center justify-between">
                  <div className="flex items-center gap-3">
                    <div className="w-10 h-10 bg-gradient-to-r from-purple-500 to-pink-500 rounded-full flex items-center justify-center text-white font-bold">
                      {suggestion.avatar}
                    </div>
                    <div>
                      <div className={`font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>{suggestion.name}</div>
                      <div className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>{suggestion.username}</div>
                    </div>
                  </div>
                  <button
                    className={`px-3 py-1 rounded-full text-sm font-bold ${
                      suggestion.following 
                        ? `${isDarkMode ? 'bg-gray-700 text-gray-300' : 'bg-gray-200 text-gray-700'}`
                        : `${isDarkMode ? 'bg-blue-600 text-white hover:bg-blue-700' : 'bg-blue-500 text-white hover:bg-blue-600'}`
                    } transition-colors`}
                  >
                    {suggestion.following ? 'Following' : 'Follow'}
                  </button>
                </div>
              ))}
            </div>
          </div>

          {/* Gaming Stats */}
          <div className={`p-4 rounded-xl ${isDarkMode ? 'bg-black bg-opacity-30' : 'bg-white bg-opacity-70'} backdrop-blur-sm`}>
            <h3 className={`text-lg font-bold mb-4 flex items-center gap-2 ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>
              <Gamepad2 size={20} className="text-purple-500" />
              Your Gaming Stats
            </h3>
            <div className="space-y-3">
              <div className="flex justify-between">
                <span className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>Games Played</span>
                <span className={`font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>147</span>
              </div>
              <div className="flex justify-between">
                <span className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>Wins</span>
                <span className={`font-bold text-green-500`}>89</span>
              </div>
              <div className="flex justify-between">
                <span className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>Highest Score</span>
                <span className={`font-bold ${isDarkMode ? 'text-yellow-400' : 'text-yellow-600'}`}>2,450</span>
              </div>
              <div className="flex justify-between">
                <span className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>Crypto Traded</span>
                <span className={`font-bold ${isDarkMode ? 'text-blue-400' : 'text-blue-600'}`}>$12,780</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
};

// Background decoration component
const FunBackground = ({ isDarkMode }) => {
  const symbols = ['₿', '💰', '♠', '♥', '♦', '♣', '🎲', '🎯', '🃏', '🎰', '💎', '⚡', '⭐', '🎮', '🏆', '📈', '📉', '🏦', '💼', '📱', '💻', '🌐'];
  
  return (
    <div className="fixed inset-0 overflow-hidden pointer-events-none z-0">
      {Array.from({ length: 35 }).map((_, i) => {
        const symbol = symbols[Math.floor(Math.random() * symbols.length)];
        const size = Math.random() * 20 + 10;
        const left = Math.random() * 100;
        const top = Math.random() * 100;
        const opacity = isDarkMode ? Math.random() * 0.3 + 0.1 : Math.random() * 0.2 + 0.05;
        const rotate = Math.random() * 360;
        const delay = Math.random() * 5;
        
        return (
          <div
            key={i}
            className="absolute animate-bounce"
            style={{
              left: `${left}%`,
              top: `${top}%`,
              fontSize: `${size}px`,
              opacity: opacity,
              transform: `rotate(${rotate}deg)`,
              animationDelay: `${delay}s`,
              animationDuration: `${3 + Math.random() * 4}s`,
              color: isDarkMode ? 'rgba(255,255,255,0.7)' : 'rgba(0,0,0,0.3)'
            }}
          >
            {symbol}
          </div>
        );
      })}
      
      {/* Floating poker chips */}
      {Array.from({ length: 18 }).map((_, i) => {
        const colors = ['bg-red-500', 'bg-blue-500', 'bg-green-500', 'bg-purple-500', 'bg-yellow-500'];
        const color = colors[Math.floor(Math.random() * colors.length)];
        const left = Math.random() * 100;
        const top = Math.random() * 100;
        const size = Math.random() * 30 + 20;
        const delay = Math.random() * 5;
        const opacity = isDarkMode ? 0.1 : 0.05;
        
        return (
          <div
            key={`chip-${i}`}
            className={`absolute rounded-full ${color} opacity-${isDarkMode ? '10' : '5'} animate-pulse`}
            style={{
              left: `${left}%`,
              top: `${top}%`,
              width: `${size}px`,
              height: `${size}px`,
              animationDelay: `${delay}s`,
              animationDuration: `${4 + Math.random() * 3}s`,
              opacity: opacity
            }}
          />
        );
      })}
    </div>
  );
};

// Share Modal Component
const ShareModal = ({ isOpen, onClose, totalScore, isDarkMode }) => {
  const [copied, setCopied] = useState(false);
  
  const shareText = `I just scored ${totalScore} points on Bilpcoin Fun! 🎮💰 Join me in the ultimate gaming experience with 11 amazing games and social chat! #BilpcoinFun #Gaming #CryptoGaming`;
  const shareUrl = 'https://bilpcoin.fun';
  
  const copyToClipboard = () => {
    navigator.clipboard.writeText(`${shareText} ${shareUrl}`);
    setCopied(true);
    setTimeout(() => setCopied(false), 2000);
  };
  
  const shareToSocial = (platform) => {
    const urls = {
      twitter: `https://twitter.com/intent/tweet?text=${encodeURIComponent(shareText)}&url=${encodeURIComponent(shareUrl)}`,
      facebook: `https://www.facebook.com/sharer/sharer.php?u=${encodeURIComponent(shareUrl)}`,
      instagram: 'https://www.instagram.com/',
      linkedin: `https://www.linkedin.com/sharing/share-offsite/?url=${encodeURIComponent(shareUrl)}`
    };
    
    if (urls[platform]) {
      window.open(urls[platform], '_blank', 'width=600,height=400');
    }
  };
  
  if (!isOpen) return null;
  
  return (
    <div className={`fixed inset-0 ${isDarkMode ? 'bg-black bg-opacity-50' : 'bg-gray-800 bg-opacity-50'} flex items-center justify-center z-50 p-4`}>
      <div className={`${isDarkMode ? 'bg-gradient-to-br from-purple-900 to-indigo-900' : 'bg-gradient-to-br from-purple-100 to-indigo-100'} rounded-2xl p-6 max-w-md w-full border border-yellow-400 border-opacity-30`}>
        <div className="flex justify-between items-center mb-4">
          <h3 className={`text-2xl font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'} flex items-center gap-2`}>
            <Share2 size={24} className="text-yellow-400" />
            Share Your Score!
          </h3>
          <button
            onClick={onClose}
            className={`${isDarkMode ? 'text-gray-400 hover:text-white' : 'text-gray-500 hover:text-gray-800'} transition-colors`}
          >
            ✕
          </button>
        </div>
        
        <div className="text-center mb-6">
          <div className="text-4xl font-bold text-yellow-400 mb-2">{totalScore}</div>
          <div className={`${isDarkMode ? 'text-purple-200' : 'text-purple-600'}`}>Total Points</div>
        </div>
        
        <div className="grid grid-cols-2 gap-3 mb-4">
          <button
            onClick={() => shareToSocial('twitter')}
            className="flex flex-col items-center gap-2 p-3 bg-gradient-to-r from-blue-500 to-blue-700 text-white rounded-xl hover:from-blue-600 hover:to-blue-800 transform hover:scale-105 transition-all duration-200"
          >
            <Twitter size={24} />
            <span className="text-sm">Twitter</span>
          </button>
          <button
            onClick={() => shareToSocial('facebook')}
            className="flex flex-col items-center gap-2 p-3 bg-gradient-to-r from-blue-700 to-blue-900 text-white rounded-xl hover:from-blue-800 hover:to-blue-900 transform hover:scale-105 transition-all duration-200"
          >
            <Facebook size={24} />
            <span className="text-sm">Facebook</span>
          </button>
          <button
            onClick={() => shareToSocial('instagram')}
            className="flex flex-col items-center gap-2 p-3 bg-gradient-to-r from-pink-500 to-pink-700 text-white rounded-xl hover:from-pink-600 hover:to-pink-800 transform hover:scale-105 transition-all duration-200"
          >
            <Instagram size={24} />
            <span className="text-sm">Instagram</span>
          </button>
          <button
            onClick={() => shareToSocial('linkedin')}
            className="flex flex-col items-center gap-2 p-3 bg-gradient-to-r from-blue-600 to-blue-800 text-white rounded-xl hover:from-blue-700 hover:to-blue-900 transform hover:scale-105 transition-all duration-200"
          >
            <Linkedin size={24} />
            <span className="text-sm">LinkedIn</span>
          </button>
        </div>
        
        <button
          onClick={copyToClipboard}
          className="w-full flex items-center justify-center gap-2 p-3 bg-gradient-to-r from-green-500 to-green-700 text-white rounded-xl hover:from-green-600 hover:to-green-800 transform hover:scale-105 transition-all duration-200"
        >
          {copied ? <Check size={20} /> : <Copy size={20} />}
          {copied ? 'Copied!' : 'Copy Link'}
        </button>
      </div>
    </div>
  );
};

// Existing game components remain the same with isDarkMode prop
// Card Game Components
const suits = ['♠', '♥', '♦', '♣'];
const ranks = ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'];
const colors = { '♠': 'text-gray-800', '♣': 'text-gray-800', '♥': 'text-red-500', '♦': 'text-red-500' };

const createDeck = () => {
  const deck = [];
  for (const suit of suits) {
    for (const rank of ranks) {
      deck.push({ suit, rank, id: `${suit}-${rank}` });
    }
  }
  return deck;
};

const shuffleDeck = (deck) => {
  const shuffled = [...deck];
  for (let i = shuffled.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
  }
  return shuffled;
};

const getCardValue = (card) => {
  if (card.rank === 'A') return 11;
  if (['J', 'Q', 'K'].includes(card.rank)) return 10;
  return parseInt(card.rank);
};

const CardComponent = ({ card, isFlipped = false, isHighlighted = false, onClick }) => {
  if (isFlipped) {
    return (
      <div 
        className="w-14 h-20 bg-gradient-to-br from-blue-600 to-purple-700 rounded-lg shadow-lg flex items-center justify-center cursor-pointer transform transition-all duration-300 hover:scale-105"
        onClick={onClick}
      >
        <div className="text-white font-bold text-sm">?</div>
      </div>
    );
  }

  return (
    <div 
      className={`w-14 h-20 bg-white rounded-lg shadow-lg border-2 flex flex-col items-center justify-between p-1 cursor-pointer transform transition-all duration-300 hover:scale-105 ${
        isHighlighted ? 'ring-2 ring-yellow-400 ring-opacity-75' : ''
      }`}
      onClick={onClick}
    >
      <div className={`text-xs font-bold ${colors[card.suit]}`}>{card.rank}</div>
      <div className={`text-lg ${colors[card.suit]}`}>{card.suit}</div>
      <div className={`text-xs font-bold ${colors[card.suit]} rotate-180`}>{card.rank}</div>
    </div>
  );
};

// Dice Game Component
const DiceGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [dice1, setDice1] = useState(1);
  const [dice2, setDice2] = useState(1);
  const [rollCount, setRollCount] = useState(0);
  const [isRolling, setIsRolling] = useState(false);

  const rollDice = () => {
    if (isRolling || rollCount >= 3) return;
    setIsRolling(true);
    
    let rolls = 0;
    const rollInterval = setInterval(() => {
      setDice1(Math.floor(Math.random() * 6) + 1);
      setDice2(Math.floor(Math.random() * 6) + 1);
      rolls++;
      if (rolls > 10) {
        clearInterval(rollInterval);
        const finalDice1 = Math.floor(Math.random() * 6) + 1;
        const finalDice2 = Math.floor(Math.random() * 6) + 1;
        setDice1(finalDice1);
        setDice2(finalDice2);
        const score = finalDice1 + finalDice2;
        setRollCount(prev => prev + 1);
        onScoreUpdate(score, 3 - rollCount);
        setIsRolling(false);
      }
    }, 100);
  };

  const resetGame = () => {
    setDice1(1);
    setDice2(1);
    setRollCount(0);
  };

  if (!isActive) return null;

  return (
    <div className="text-center">
      <div className="flex justify-center gap-4 mb-6">
        <div className="w-16 h-16 bg-white rounded-xl shadow-lg flex items-center justify-center text-3xl font-bold">
          {dice1}
        </div>
        <div className="w-16 h-16 bg-white rounded-xl shadow-lg flex items-center justify-center text-3xl font-bold">
          {dice2}
        </div>
      </div>
      <button
        onClick={rollDice}
        disabled={isRolling || rollCount >= 3}
        className="px-6 py-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white rounded-full font-bold shadow-lg hover:from-green-600 hover:to-emerald-700 transform hover:scale-105 transition-all duration-200 disabled:opacity-50 disabled:cursor-not-allowed"
      >
        {rollCount < 3 ? `Roll Dice (${3 - rollCount} left)` : 'No Rolls Left'}
      </button>
      <button
        onClick={resetGame}
        className="ml-4 px-4 py-2 bg-gradient-to-r from-gray-500 to-gray-600 text-white rounded-full font-bold shadow-lg hover:from-gray-600 hover:to-gray-700 transform hover:scale-105 transition-all duration-200"
      >
        Reset
      </button>
    </div>
  );
};

// Memory Game Component
const MemoryGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const emojis = ['😀', '😎', '🤩', '🥳', '😍', '🥰', '🥳', '🤩', '😎', '😀', '😍', '🥰'];
  const [cards, setCards] = useState([]);
  const [flippedCards, setFlippedCards] = useState([]);
  const [matchedPairs, setMatchedPairs] = useState(0);
  const [moves, setMoves] = useState(0);
  const [gameCompleted, setGameCompleted] = useState(false);

  const initializeGame = () => {
    const shuffled = [...emojis].sort(() => Math.random() - 0.5);
    const gameCards = shuffled.map((emoji, index) => ({
      id: index,
      emoji,
      isFlipped: false,
      isMatched: false
    }));
    setCards(gameCards);
    setFlippedCards([]);
    setMatchedPairs(0);
    setMoves(0);
    setGameCompleted(false);
  };

  useEffect(() => {
    if (isActive) {
      initializeGame();
    }
  }, [isActive]);

  const flipCard = (id) => {
    if (gameCompleted || flippedCards.length >= 2 || cards[id].isFlipped || cards[id].isMatched) {
      return;
    }

    const updatedCards = [...cards];
    updatedCards[id].isFlipped = true;
    setCards(updatedCards);
    setFlippedCards(prev => [...prev, id]);

    if (flippedCards.length === 1) {
      const firstCard = cards[flippedCards[0]];
      const secondCard = cards[id];
      setMoves(prev => prev + 1);

      if (firstCard.emoji === secondCard.emoji) {
        updatedCards[flippedCards[0]].isMatched = true;
        updatedCards[id].isMatched = true;
        setCards(updatedCards);
        setMatchedPairs(prev => prev + 1);
        setFlippedCards([]);
        
        if (matchedPairs + 1 === emojis.length / 2) {
          setGameCompleted(true);
          const score = Math.max(100 - moves * 5, 10);
          onScoreUpdate(score, 0);
        }
      } else {
        setTimeout(() => {
          const resetCards = [...cards];
          resetCards[flippedCards[0]].isFlipped = false;
          resetCards[id].isFlipped = false;
          setCards(resetCards);
          setFlippedCards([]);
        }, 1000);
      }
    }
  };

  if (!isActive) return null;

  return (
    <div className="text-center">
      <div className="grid grid-cols-4 gap-3 max-w-md mx-auto mb-6">
        {cards.map((card) => (
          <div
            key={card.id}
            onClick={() => flipCard(card.id)}
            className="w-16 h-16 bg-gradient-to-br from-blue-500 to-purple-600 rounded-lg shadow-lg flex items-center justify-center text-2xl cursor-pointer transform transition-all duration-300 hover:scale-105"
          >
            {card.isFlipped || card.isMatched ? card.emoji : '?'}
          </div>
        ))}
      </div>
      <div className={`${isDarkMode ? 'text-gray-300' : 'text-gray-700'} mb-4`}>
        <p>Moves: {moves} | Pairs: {matchedPairs}/{emojis.length / 2}</p>
        {gameCompleted && <p className="text-green-600 font-bold">Congratulations! Game completed!</p>}
      </div>
      <button
        onClick={initializeGame}
        className="px-6 py-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white rounded-full font-bold shadow-lg hover:from-green-600 hover:to-emerald-700 transform hover:scale-105 transition-all duration-200"
      >
        New Game
      </button>
    </div>
  );
};

// Target Practice Game Component
const TargetGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [shots, setShots] = useState(0);
  const [score, setScore] = useState(0);
  const [gameActive, setGameActive] = useState(false);
  const [targets, setTargets] = useState([]);

  const startGame = () => {
    setShots(0);
    setScore(0);
    setGameActive(true);
    setTargets([]);
    const newTargets = Array.from({ length: 5 }, (_, i) => ({
      id: i,
      x: Math.random() * 80 + 10,
      y: Math.random() * 70 + 15,
      size: Math.random() * 20 + 30,
      hit: false
    }));
    setTargets(newTargets);
  };

  const shootTarget = (targetId) => {
    if (!gameActive || shots >= 5) return;
    
    const updatedTargets = targets.map(target => 
      target.id === targetId ? { ...target, hit: true } : target
    );
    setTargets(updatedTargets);
    
    const target = targets.find(t => t.id === targetId);
    const points = Math.floor(100 - (target.size / 2));
    setScore(prev => prev + points);
    setShots(prev => prev + 1);
    
    if (shots + 1 >= 5) {
      setGameActive(false);
      onScoreUpdate(score + points, 0);
    }
  };

  if (!isActive) return null;

  return (
    <div className="text-center">
      <div 
        className="relative w-full h-64 bg-gradient-to-b from-green-800 to-green-900 rounded-xl shadow-lg mb-6 border-4 border-yellow-600"
        style={{ minHeight: '256px' }}
      >
        {targets.map(target => (
          <div
            key={target.id}
            onClick={() => shootTarget(target.id)}
            className={`absolute transform -translate-x-1/2 -translate-y-1/2 rounded-full cursor-pointer transition-all duration-200 ${
              target.hit ? 'bg-red-500 scale-110' : 'bg-yellow-400 hover:bg-yellow-300'
            }`}
            style={{
              left: `${target.x}%`,
              top: `${target.y}%`,
              width: `${target.size}px`,
              height: `${target.size}px`,
              boxShadow: target.hit ? '0 0 20px red' : '0 0 10px gold'
            }}
          >
            {!target.hit && <div className="text-black font-bold text-xs">{Math.floor(100 - (target.size / 2))}</div>}
          </div>
        ))}
        {!gameActive && targets.length === 0 && (
          <div className="absolute inset-0 flex items-center justify-center">
            <p className={`${isDarkMode ? 'text-white' : 'text-gray-800'} text-xl`}>Click "Start Game" to begin!</p>
          </div>
        )}
      </div>
      <div className={`${isDarkMode ? 'text-gray-300' : 'text-gray-700'} mb-4`}>
        <p>Shots: {shots}/5 | Score: {score}</p>
      </div>
      <button
        onClick={startGame}
        disabled={gameActive}
        className="px-6 py-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white rounded-full font-bold shadow-lg hover:from-green-600 hover:to-emerald-700 transform hover:scale-105 transition-all duration-200 disabled:opacity-50"
      >
        {gameActive ? 'Game in Progress' : 'Start Game'}
      </button>
    </div>
  );
};

// Roulette Game Component
const RouletteGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [balance, setBalance] = useState(100);
  const [betAmount, setBetAmount] = useState(10);
  const [betType, setBetType] = useState('red');
  const [spinning, setSpinning] = useState(false);
  const [result, setResult] = useState(null);
  const [winAmount, setWinAmount] = useState(0);

  const numbers = Array.from({ length: 37 }, (_, i) => i);
  const redNumbers = [1, 3, 5, 7, 9, 12, 14, 16, 18, 19, 21, 23, 25, 27, 30, 32, 34, 36];
  const blackNumbers = [2, 4, 6, 8, 10, 11, 13, 15, 17, 20, 22, 24, 26, 28, 29, 31, 33, 35];

  const isRed = (num) => redNumbers.includes(num);
  const isBlack = (num) => blackNumbers.includes(num);
  const isEven = (num) => num !== 0 && num % 2 === 0;
  const isOdd = (num) => num !== 0 && num % 2 === 1;
  const is1to18 = (num) => num >= 1 && num <= 18;
  const is19to36 = (num) => num >= 19 && num <= 36;

  const spinRoulette = () => {
    if (spinning || balance < betAmount) return;
    if (betAmount <= 0) {
      alert('Please enter a valid bet amount!');
      return;
    }

    setSpinning(true);
    setBalance(prev => prev - betAmount);

    let spins = 0;
    const spinInterval = setInterval(() => {
      const randomResult = Math.floor(Math.random() * 37);
      setResult(randomResult);
      spins++;
      if (spins > 20) {
        clearInterval(spinInterval);
        const finalResult = Math.floor(Math.random() * 37);
        setResult(finalResult);
        
        let won = false;
        let multiplier = 2;
        
        switch (betType) {
          case 'red':
            won = isRed(finalResult);
            break;
          case 'black':
            won = isBlack(finalResult);
            break;
          case 'even':
            won = isEven(finalResult);
            break;
          case 'odd':
            won = isOdd(finalResult);
            break;
          case '1-18':
            won = is1to18(finalResult);
            break;
          case '19-36':
            won = is19to36(finalResult);
            break;
          default:
            won = false;
        }

        if (won) {
          const winnings = betAmount * multiplier;
          setBalance(prev => prev + winnings);
          setWinAmount(winnings);
          onScoreUpdate(winnings, 0);
        } else {
          setWinAmount(0);
        }
        setSpinning(false);
      }
    }, 100);
  };

  const resetGame = () => {
    setBalance(100);
    setResult(null);
    setWinAmount(0);
  };

  if (!isActive) return null;

  const getNumberColor = (num) => {
    if (num === 0) return 'text-green-600';
    return isRed(num) ? 'text-red-600' : 'text-gray-800';
  };

  return (
    <div className="text-center">
      <div className="mb-6">
        <div className={`text-2xl font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'} mb-2`}>Balance: ${balance}</div>
        {result !== null && (
          <div className={`text-xl font-bold mb-2 ${winAmount > 0 ? 'text-green-600' : 'text-red-600'}`}>
            {result === 0 ? (
              <span className="text-green-600">0</span>
            ) : (
              <span className={getNumberColor(result)}>{result}</span>
            )}
            {winAmount > 0 ? ` - Won $${winAmount}!` : ' - Better luck next time!'}
          </div>
        )}
      </div>

      <div className="flex justify-center gap-4 mb-6">
        <input
          type="number"
          value={betAmount}
          onChange={(e) => setBetAmount(Math.max(1, Math.min(500, parseInt(e.target.value) || 1)))}
          className={`w-24 px-3 py-2 ${isDarkMode ? 'bg-gray-700 text-white' : 'bg-white text-gray-800'} rounded-lg`}
          min="1"
          max="500"
        />
        <select
          value={betType}
          onChange={(e) => setBetType(e.target.value)}
          className={`px-3 py-2 ${isDarkMode ? 'bg-gray-700 text-white' : 'bg-white text-gray-800'} rounded-lg`}
        >
          <option value="red">Red (1:1)</option>
          <option value="black">Black (1:1)</option>
          <option value="even">Even (1:1)</option>
          <option value="odd">Odd (1:1)</option>
          <option value="1-18">1-18 (1:1)</option>
          <option value="19-36">19-36 (1:1)</option>
        </select>
      </div>

      <button
        onClick={spinRoulette}
        disabled={spinning || balance < betAmount}
        className="px-6 py-3 bg-gradient-to-r from-red-600 to-red-800 text-white rounded-full font-bold shadow-lg hover:from-red-700 hover:to-red-900 transform hover:scale-105 transition-all duration-200 disabled:opacity-50"
      >
        {spinning ? 'Spinning...' : `Spin Roulette ($${betAmount})`}
      </button>

      <button
        onClick={resetGame}
        className="ml-4 px-4 py-3 bg-gradient-to-r from-gray-600 to-gray-800 text-white rounded-full font-bold shadow-lg hover:from-gray-700 hover:to-gray-900 transform hover:scale-105 transition-all duration-200"
      >
        Reset
      </button>

      <div className="mt-6 grid grid-cols-6 gap-1 max-w-md mx-auto">
        {numbers.map(num => (
          <div
            key={num}
            className={`w-10 h-10 rounded flex items-center justify-center font-bold text-sm ${
              num === 0 
                ? 'bg-green-600 text-white' 
                : isRed(num) 
                  ? 'bg-red-100 text-red-600' 
                  : 'bg-gray-100 text-gray-800'
            } ${num === result ? 'ring-2 ring-yellow-400 ring-opacity-75 scale-110' : ''}`}
          >
            {num}
          </div>
        ))}
      </div>
    </div>
  );
};

// Rock Paper Scissors Game Component
const RockPaperScissorsGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [playerChoice, setPlayerChoice] = useState(null);
  const [computerChoice, setComputerChoice] = useState(null);
  const [result, setResult] = useState('');
  const [playerScore, setPlayerScore] = useState(0);
  const [computerScore, setComputerScore] = useState(0);
  const [round, setRound] = useState(0);
  const [gameOver, setGameOver] = useState(false);

  const choices = ['rock', 'paper', 'scissors'];
  const choiceIcons = {
    rock: <div className="w-12 h-12 bg-gray-600 rounded-full flex items-center justify-center text-white">✊</div>,
    paper: <div className="w-12 h-12 bg-blue-600 rounded-full flex items-center justify-center text-white">✋</div>,
    scissors: <div className="w-12 h-12 bg-red-600 rounded-full flex items-center justify-center text-white">✌️</div>
  };

  const getWinner = (player, computer) => {
    if (player === computer) return 'tie';
    if (
      (player === 'rock' && computer === 'scissors') ||
      (player === 'paper' && computer === 'rock') ||
      (player === 'scissors' && computer === 'paper')
    ) {
      return 'player';
    }
    return 'computer';
  };

  const playRound = (choice) => {
    if (gameOver || round >= 5) return;
    
    const computerChoice = choices[Math.floor(Math.random() * choices.length)];
    setPlayerChoice(choice);
    setComputerChoice(computerChoice);
    
    const winner = getWinner(choice, computerChoice);
    let roundResult = '';
    
    if (winner === 'player') {
      setPlayerScore(prev => prev + 1);
      roundResult = 'You win this round!';
      onScoreUpdate(20, 0);
    } else if (winner === 'computer') {
      setComputerScore(prev => prev + 1);
      roundResult = 'Computer wins this round!';
    } else {
      roundResult = 'It\'s a tie!';
    }
    
    setResult(roundResult);
    setRound(prev => prev + 1);
    
    if (round + 1 >= 5) {
      setGameOver(true);
      if (playerScore > computerScore) {
        onScoreUpdate(100, 0);
      }
    }
  };

  const resetGame = () => {
    setPlayerChoice(null);
    setComputerChoice(null);
    setResult('');
    setPlayerScore(0);
    setComputerScore(0);
    setRound(0);
    setGameOver(false);
  };

  if (!isActive) return null;

  return (
    <div className="text-center">
      <div className="mb-6">
        <div className="flex justify-center gap-8 mb-4">
          <div className="text-center">
            <div className={`font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>Player: {playerScore}</div>
            {playerChoice && choiceIcons[playerChoice]}
          </div>
          <div className="text-center">
            <div className={`font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>Round {round}/5</div>
            {round > 0 && <div className="text-yellow-600 font-bold">{result}</div>}
          </div>
          <div className="text-center">
            <div className={`font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>Computer: {computerScore}</div>
            {computerChoice && choiceIcons[computerChoice]}
          </div>
        </div>
      </div>

      {!gameOver && round < 5 && (
        <div className="flex justify-center gap-4 mb-6">
          {choices.map(choice => (
            <button
              key={choice}
              onClick={() => playRound(choice)}
              className="p-4 bg-gradient-to-r from-purple-600 to-blue-700 text-white rounded-full font-bold shadow-lg hover:from-purple-700 hover:to-blue-800 transform hover:scale-105 transition-all duration-200"
            >
              {choice.charAt(0).toUpperCase() + choice.slice(1)}
            </button>
          ))}
        </div>
      )}

      {gameOver && (
        <div className="mb-6">
          <div className={`text-2xl font-bold ${playerScore > computerScore ? 'text-green-600' : playerScore < computerScore ? 'text-red-600' : 'text-yellow-600'}`}>
            {playerScore > computerScore ? 'You Win!' : playerScore < computerScore ? 'Computer Wins!' : 'It\'s a Tie!'}
          </div>
        </div>
      )}

      <button
        onClick={resetGame}
        className="px-6 py-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white rounded-full font-bold shadow-lg hover:from-green-600 hover:to-emerald-700 transform hover:scale-105 transition-all duration-200"
      >
        {gameOver ? 'Play Again' : 'Reset Game'}
      </button>
    </div>
  );
};

// Number Guessing Game
const NumberGuessingGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [targetNumber, setTargetNumber] = useState(0);
  const [guess, setGuess] = useState('');
  const [attempts, setAttempts] = useState(0);
  const [message, setMessage] = useState('Guess a number between 1-100!');
  const [gameOver, setGameOver] = useState(false);
  const [maxAttempts] = useState(7);

  const startNewGame = () => {
    setTargetNumber(Math.floor(Math.random() * 100) + 1);
    setGuess('');
    setAttempts(0);
    setMessage('Guess a number between 1-100!');
    setGameOver(false);
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (gameOver || attempts >= maxAttempts) return;
    
    const numGuess = parseInt(guess);
    if (isNaN(numGuess) || numGuess < 1 || numGuess > 100) {
      setMessage('Please enter a number between 1-100!');
      return;
    }
    
    setAttempts(prev => prev + 1);
    
    if (numGuess === targetNumber) {
      const score = Math.max(100 - (attempts * 10), 20);
      setMessage(`🎉 Correct! The number was ${targetNumber}. You got it in ${attempts + 1} attempts!`);
      setGameOver(true);
      onScoreUpdate(score, 0);
    } else if (numGuess < targetNumber) {
      setMessage(`Too low! (${maxAttempts - attempts - 1} attempts left)`);
    } else {
      setMessage(`Too high! (${maxAttempts - attempts - 1} attempts left)`);
    }
    
    if (attempts + 1 >= maxAttempts) {
      setMessage(`Game over! The number was ${targetNumber}. Better luck next time!`);
      setGameOver(true);
    }
    
    setGuess('');
  };

  useEffect(() => {
    if (isActive) {
      startNewGame();
    }
  }, [isActive]);

  if (!isActive) return null;

  return (
    <div className="text-center">
      <div className="mb-6">
        <div className={`${isDarkMode ? 'text-gray-300' : 'text-gray-700'} text-lg mb-2`}>Attempts: {attempts}/{maxAttempts}</div>
        <div className="text-yellow-600 font-bold">{message}</div>
      </div>
      
      {!gameOver && attempts < maxAttempts && (
        <form onSubmit={handleSubmit} className="mb-6">
          <input
            type="number"
            value={guess}
            onChange={(e) => setGuess(e.target.value)}
            className={`w-32 px-4 py-2 ${isDarkMode ? 'bg-gray-700 text-white' : 'bg-white text-gray-800'} rounded-lg mr-2`}
            min="1"
            max="100"
            placeholder="1-100"
          />
          <button
            type="submit"
            className="px-4 py-2 bg-gradient-to-r from-blue-500 to-indigo-600 text-white rounded-lg font-bold hover:from-blue-600 hover:to-indigo-700 transform hover:scale-105 transition-all duration-200"
          >
            Guess
          </button>
        </form>
      )}
      
      <button
        onClick={startNewGame}
        className="px-6 py-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white rounded-full font-bold shadow-lg hover:from-green-600 hover:to-emerald-700 transform hover:scale-105 transition-all duration-200"
      >
        New Game
      </button>
    </div>
  );
};

// Tic Tac Toe Game
const TicTacToeGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [board, setBoard] = useState(Array(9).fill(null));
  const [isXNext, setIsXNext] = useState(true);
  const [winner, setWinner] = useState(null);
  const [xScore, setXScore] = useState(0);
  const [oScore, setOScore] = useState(0);

  const calculateWinner = (squares) => {
    const lines = [
      [0, 1, 2], [3, 4, 5], [6, 7, 8],
      [0, 3, 6], [1, 4, 7], [2, 5, 8],
      [0, 4, 8], [2, 4, 6]
    ];
    for (let i = 0; i < lines.length; i++) {
      const [a, b, c] = lines[i];
      if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
        return squares[a];
      }
    }
    return squares.every(square => square !== null) ? 'draw' : null;
  };

  const handleClick = (index) => {
    if (winner || board[index] || !isActive) return;
    
    const newBoard = [...board];
    newBoard[index] = isXNext ? 'X' : 'O';
    setBoard(newBoard);
    setIsXNext(!isXNext);
    
    const gameWinner = calculateWinner(newBoard);
    if (gameWinner) {
      setWinner(gameWinner);
      if (gameWinner === 'X') {
        setXScore(prev => prev + 1);
        onScoreUpdate(50, 0);
      } else if (gameWinner === 'O') {
        setOScore(prev => prev + 1);
        onScoreUpdate(50, 0);
      }
    }
  };

  const resetGame = () => {
    setBoard(Array(9).fill(null));
    setIsXNext(true);
    setWinner(null);
  };

  const resetScores = () => {
    resetGame();
    setXScore(0);
    setOScore(0);
  };

  if (!isActive) return null;

  const getStatusMessage = () => {
    if (winner === 'draw') return "It's a draw!";
    if (winner) return `Player ${winner} wins!`;
    return `Next player: ${isXNext ? 'X' : 'O'}`;
  };

  return (
    <div className="text-center">
      <div className="mb-6">
        <div className={`${isDarkMode ? 'text-white' : 'text-gray-800'} text-lg mb-2`}>
          Scores - X: {xScore} | O: {oScore}
        </div>
        <div className={`font-bold ${winner ? (winner === 'draw' ? 'text-yellow-600' : 'text-green-600') : isDarkMode ? 'text-white' : 'text-gray-800'}`}>
          {getStatusMessage()}
        </div>
      </div>
      
      <div className="grid grid-cols-3 gap-2 max-w-xs mx-auto mb-6">
        {board.map((square, index) => (
          <button
            key={index}
            onClick={() => handleClick(index)}
            className="w-16 h-16 bg-gradient-to-br from-purple-600 to-blue-700 text-white text-3xl font-bold rounded-lg shadow-lg hover:from-purple-700 hover:to-blue-800 transform hover:scale-105 transition-all duration-200 flex items-center justify-center"
          >
            {square}
          </button>
        ))}
      </div>
      
      <div className="flex justify-center gap-4">
        <button
          onClick={resetGame}
          className="px-4 py-2 bg-gradient-to-r from-gray-500 to-gray-600 text-white rounded-lg font-bold hover:from-gray-600 hover:to-gray-700 transform hover:scale-105 transition-all duration-200"
        >
          New Game
        </button>
        <button
          onClick={resetScores}
          className="px-4 py-2 bg-gradient-to-r from-red-500 to-red-600 text-white rounded-lg font-bold hover:from-red-600 hover:to-red-700 transform hover:scale-105 transition-all duration-200"
        >
          Reset Scores
        </button>
      </div>
    </div>
  );
};

// Whack-a-Mole Game
const WhackAMoleGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [score, setScore] = useState(0);
  const [timeLeft, setTimeLeft] = useState(30);
  const [gameActive, setGameActive] = useState(false);
  const [moles, setMoles] = useState(Array(9).fill(false));
  const [gameOver, setGameOver] = useState(false);

  const startGame = () => {
    setScore(0);
    setTimeLeft(30);
    setGameActive(true);
    setGameOver(false);
    setMoles(Array(9).fill(false));
  };

  const whackMole = (index) => {
    if (!gameActive || !moles[index]) return;
    setScore(prev => prev + 10);
    setMoles(prev => {
      const newMoles = [...prev];
      newMoles[index] = false;
      return newMoles;
    });
  };

  useEffect(() => {
    if (!isActive) return;
    
    let moleInterval, timerInterval;
    
    if (gameActive) {
      moleInterval = setInterval(() => {
        setMoles(prev => {
          const newMoles = [...prev];
          newMoles.forEach((_, i) => {
            if (Math.random() < 0.3) newMoles[i] = false;
          });
          const randomIndex = Math.floor(Math.random() * 9);
          newMoles[randomIndex] = true;
          return newMoles;
        });
      }, 1000);
      
      timerInterval = setInterval(() => {
        setTimeLeft(prev => {
          if (prev <= 1) {
            setGameActive(false);
            setGameOver(true);
            onScoreUpdate(score, 0);
            return 0;
          }
          return prev - 1;
        });
      }, 1000);
    }
    
    return () => {
      if (moleInterval) clearInterval(moleInterval);
      if (timerInterval) clearInterval(timerInterval);
    };
  }, [gameActive, isActive, score, onScoreUpdate]);

  if (!isActive) return null;

  return (
    <div className="text-center">
      <div className="mb-6">
        <div className={`${isDarkMode ? 'text-gray-300' : 'text-gray-700'} text-xl mb-2`}>Score: {score}</div>
        <div className={`text-2xl font-bold ${gameActive ? 'text-green-600' : gameOver ? 'text-red-600' : isDarkMode ? 'text-white' : 'text-gray-800'}`}>
          {gameActive ? `Time: ${timeLeft}s` : gameOver ? 'Game Over!' : 'Click Start to Play!'}
        </div>
      </div>
      
      <div className="grid grid-cols-3 gap-2 max-w-xs mx-auto mb-6">
        {moles.map((isUp, index) => (
          <button
            key={index}
            onClick={() => whackMole(index)}
            className={`w-16 h-16 rounded-lg shadow-lg transform transition-all duration-200 ${
              isUp 
                ? 'bg-gradient-to-b from-yellow-400 to-orange-500 scale-110 ring-4 ring-yellow-300' 
                : 'bg-gradient-to-b from-green-700 to-green-800'
            }`}
          >
            {isUp && '🐹'}
          </button>
        ))}
      </div>
      
      <button
        onClick={startGame}
        disabled={gameActive}
        className="px-6 py-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white rounded-full font-bold shadow-lg hover:from-green-600 hover:to-emerald-700 transform hover:scale-105 transition-all duration-200 disabled:opacity-50"
      >
        {gameActive ? 'Game in Progress' : 'Start Game'}
      </button>
    </div>
  );
};

// Wordle-like Game
const WordleGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const words = ['GAMES', 'FUNNY', 'BILPC', 'COINS', 'LUCKY', 'WINNER', 'PLAYER', 'SCORE', 'CHANCE', 'EXCITE'];
  const [targetWord, setTargetWord] = useState('');
  const [currentGuess, setCurrentGuess] = useState('');
  const [guesses, setGuesses] = useState([]);
  const [gameOver, setGameOver] = useState(false);
  const [gameWon, setGameWon] = useState(false);
  const [attempts, setAttempts] = useState(0);
  const maxAttempts = 6;

  const startNewGame = () => {
    const randomWord = words[Math.floor(Math.random() * words.length)];
    setTargetWord(randomWord);
    setCurrentGuess('');
    setGuesses([]);
    setGameOver(false);
    setGameWon(false);
    setAttempts(0);
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (gameOver || currentGuess.length !== 5 || attempts >= maxAttempts) return;
    
    const newGuesses = [...guesses, currentGuess.toUpperCase()];
    setGuesses(newGuesses);
    setAttempts(prev => prev + 1);
    setCurrentGuess('');
    
    if (currentGuess.toUpperCase() === targetWord) {
      setGameWon(true);
      setGameOver(true);
      const score = Math.max(100 - (attempts * 10), 20);
      onScoreUpdate(score, 0);
    } else if (attempts + 1 >= maxAttempts) {
      setGameOver(true);
    }
  };

  const getLetterClass = (letter, index, guess) => {
    if (letter === targetWord[index]) return 'bg-green-500';
    if (targetWord.includes(letter)) return 'bg-yellow-500';
    return 'bg-gray-500';
  };

  useEffect(() => {
    if (isActive) {
      startNewGame();
    }
  }, [isActive]);

  if (!isActive) return null;

  return (
    <div className="text-center">
      <div className="mb-6">
        <div className={`${isDarkMode ? 'text-gray-300' : 'text-gray-700'} text-lg mb-2`}>Attempts: {attempts}/{maxAttempts}</div>
        {gameOver && (
          <div className={`text-xl font-bold ${gameWon ? 'text-green-600' : 'text-red-600'}`}>
            {gameWon ? '🎉 You Won!' : `Game Over! Word was: ${targetWord}`}
          </div>
        )}
      </div>
      
      <div className="mb-6">
        {guesses.map((guess, guessIndex) => (
          <div key={guessIndex} className="flex justify-center gap-1 mb-1">
            {guess.split('').map((letter, letterIndex) => (
              <div
                key={letterIndex}
                className={`w-10 h-10 ${getLetterClass(letter, letterIndex, guess)} text-white font-bold rounded flex items-center justify-center`}
              >
                {letter}
              </div>
            ))}
          </div>
        ))}
        {!gameOver && (
          <div className="flex justify-center gap-1">
            {currentGuess.padEnd(5, '_').split('').map((char, index) => (
              <div
                key={index}
                className={`w-10 h-10 ${isDarkMode ? 'bg-gray-700' : 'bg-gray-200'} text-${isDarkMode ? 'white' : 'gray-800'} font-bold rounded flex items-center justify-center`}
              >
                {char !== '_' ? char : ''}
              </div>
            ))}
          </div>
        )}
      </div>
      
      {!gameOver && (
        <form onSubmit={handleSubmit} className="mb-4">
          <input
            type="text"
            value={currentGuess}
            onChange={(e) => setCurrentGuess(e.target.value.slice(0, 5).toUpperCase())}
            className={`w-40 px-4 py-2 ${isDarkMode ? 'bg-gray-700 text-white' : 'bg-white text-gray-800'} rounded-lg mr-2 text-center font-bold text-xl`}
            placeholder="5 letters"
            maxLength={5}
          />
          <button
            type="submit"
            className="px-4 py-2 bg-gradient-to-r from-blue-500 to-indigo-600 text-white rounded-lg font-bold hover:from-blue-600 hover:to-indigo-700 transform hover:scale-105 transition-all duration-200"
          >
            Guess
          </button>
        </form>
      )}
      
      <button
        onClick={startNewGame}
        className="px-6 py-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white rounded-full font-bold shadow-lg hover:from-green-600 hover:to-emerald-700 transform hover:scale-105 transition-all duration-200"
      >
        New Game
      </button>
    </div>
  );
};

// Bilpcoin Fun Chat (Original Twitter Clone)
const BilpcoinFunChat = ({ isActive, isDarkMode }) => {
  const [posts, setPosts] = useState([]);
  const [newPost, setNewPost] = useState('');
  const [user, setUser] = useState({ name: 'Bilpcoin User', username: '@bilpcoin_user' });
  const [trending, setTrending] = useState(['#Bilpcoin', '#FunGames', '#Gaming', '#WinBig', '#CryptoFun', '#StockMarket', '#Trading']);
  const [likes, setLikes] = useState({});
  const messagesEndRef = useRef(null);

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!newPost.trim()) return;
    
    const post = {
      id: Date.now(),
      content: newPost,
      timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
      likes: 0,
      user: user
    };
    
    setPosts(prev => [post, ...prev]);
    setNewPost('');
  };

  const handleLike = (postId) => {
    setLikes(prev => ({
      ...prev,
      [postId]: (prev[postId] || 0) + 1
    }));
  };

  const scrollToBottom = () => {
    messagesEndRef.current?.scrollIntoView({ behavior: "smooth" });
  };

  useEffect(() => {
    if (isActive) {
      const initialPosts = [
        { id: 1, content: "Just won the Card Challenge! Bilpcoin Fun is amazing! 🎮", timestamp: "2:30 PM", likes: 12, user: { name: "CryptoGamer", username: "@crypto_gamer" } },
        { id: 2, content: "The Roulette game is so much fun! Hit a lucky streak today 💰", timestamp: "1:15 PM", likes: 8, user: { name: "LuckyPlayer", username: "@lucky_player" } },
        { id: 3, content: "Who else is addicted to Whack-a-Mole? Can't stop playing! 🐹", timestamp: "12:45 PM", likes: 15, user: { name: "GameMaster", username: "@game_master" } },
        { id: 4, content: "Made $500 in the Crypto Trading Simulator! 📈 #BilpcoinTrading", timestamp: "11:20 AM", likes: 23, user: { name: "CryptoTrader", username: "@crypto_trader" } }
      ];
      setPosts(initialPosts);
    }
  }, [isActive]);

  useEffect(() => {
    scrollToBottom();
  }, [posts]);

  if (!isActive) return null;

  return (
    <div className="max-w-2xl mx-auto">
      <div className={`${isDarkMode ? 'bg-black bg-opacity-30' : 'bg-gray-100 bg-opacity-50'} rounded-xl p-4 mb-6 backdrop-blur-sm`}>
        <h2 className={`text-xl font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'} mb-3 flex items-center gap-2`}>
          <MessageSquare size={24} className="text-blue-500" />
          Bilpcoin Fun Chat
        </h2>
        <p className={`${isDarkMode ? 'text-purple-200' : 'text-purple-600'} text-sm mb-4`}>Share your gaming moments and connect with other players!</p>
        
        <form onSubmit={handleSubmit} className="mb-6">
          <textarea
            value={newPost}
            onChange={(e) => setNewPost(e.target.value)}
            placeholder="What's happening in your Bilpcoin Fun journey?"
            className={`w-full px-4 py-3 ${isDarkMode ? 'bg-gray-800 text-white' : 'bg-white text-gray-800'} rounded-lg mb-3 min-h-20 resize-none`}
            maxLength={280}
          />
          <div className="flex justify-between items-center">
            <div className={`${isDarkMode ? 'text-gray-400' : 'text-gray-500'} text-sm`}>{newPost.length}/280</div>
            <button
              type="submit"
              disabled={!newPost.trim()}
              className="flex items-center gap-2 px-6 py-2 bg-gradient-to-r from-blue-500 to-indigo-600 text-white rounded-full font-bold hover:from-blue-600 hover:to-indigo-700 transform hover:scale-105 transition-all duration-200 disabled:opacity-50"
            >
              <Send size={16} />
              Post
            </button>
          </div>
        </form>
        
        <div className="mb-6">
          <h3 className={`text-lg font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'} mb-3 flex items-center gap-2`}>
            <TrendingUp size={20} className="text-green-500" />
            Trending Now
          </h3>
          <div className="flex flex-wrap gap-2">
            {trending.map((topic, index) => (
              <span key={index} className="px-3 py-1 bg-gradient-to-r from-purple-500 to-pink-500 text-white rounded-full text-sm">
                {topic}
              </span>
            ))}
          </div>
        </div>
      </div>
      
      <div className="space-y-4 max-h-96 overflow-y-auto">
        {posts.map((post) => (
          <div key={post.id} className={`${isDarkMode ? 'bg-black bg-opacity-20' : 'bg-white bg-opacity-50'} rounded-xl p-4 border border-purple-500 border-opacity-30`}>
            <div className="flex items-start gap-3">
              <div className="w-10 h-10 bg-gradient-to-r from-yellow-400 to-orange-500 rounded-full flex items-center justify-center text-white font-bold">
                {post.user.name.charAt(0)}
              </div>
              <div className="flex-1">
                <div className="flex items-center gap-2 mb-2">
                  <span className={`font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>{post.user.name}</span>
                  <span className={isDarkMode ? 'text-gray-400' : 'text-gray-500'}>{post.user.username}</span>
                  <span className={isDarkMode ? 'text-gray-500' : 'text-gray-400'}>·</span>
                  <span className={`${isDarkMode ? 'text-gray-500' : 'text-gray-400'} text-sm`}>{post.timestamp}</span>
                </div>
                <p className={`${isDarkMode ? 'text-white' : 'text-gray-800'} mb-3`}>{post.content}</p>
                <button
                  onClick={() => handleLike(post.id)}
                  className="flex items-center gap-2 text-gray-500 hover:text-red-500 transition-colors"
                >
                  <Heart size={18} className={`${likes[post.id] ? 'text-red-500 fill-current' : ''}`} />
                  <span>{(post.likes + (likes[post.id] || 0)) || 'Like'}</span>
                </button>
              </div>
            </div>
          </div>
        ))}
        <div ref={messagesEndRef} />
      </div>
    </div>
  );
};

// NEW: Crypto Trading Simulator
const CryptoTradingGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [balance, setBalance] = useState(10000);
  const [portfolio, setPortfolio] = useState({});
  const [cryptoPrices, setCryptoPrices] = useState({
    BTC: 45000,
    ETH: 3200,
    SOL: 120,
    ADA: 0.55,
    DOGE: 0.12
  });
  const [selectedCrypto, setSelectedCrypto] = useState('BTC');
  const [amount, setAmount] = useState(1);
  const [leverage, setLeverage] = useState(1);
  const [position, setPosition] = useState(null); // 'long' or 'short'
  const [trades, setTrades] = useState([]);
  const [gameTime, setGameTime] = useState(0);

  // Simulate price movements
  useEffect(() => {
    if (!isActive) return;
    
    const interval = setInterval(() => {
      setCryptoPrices(prev => {
        const newPrices = {};
        Object.keys(prev).forEach(crypto => {
          const change = (Math.random() - 0.5) * 0.04; // -2% to +2%
          newPrices[crypto] = prev[crypto] * (1 + change);
        });
        return newPrices;
      });
      setGameTime(prev => prev + 1);
    }, 3000);

    return () => clearInterval(interval);
  }, [isActive]);

  const buyCrypto = () => {
    const price = cryptoPrices[selectedCrypto];
    const totalCost = price * amount * leverage;
    
    if (balance < totalCost) {
      alert('Insufficient balance!');
      return;
    }
    
    setBalance(prev => prev - totalCost);
    setPortfolio(prev => ({
      ...prev,
      [selectedCrypto]: (prev[selectedCrypto] || 0) + amount
    }));
    
    const trade = {
      id: Date.now(),
      type: 'buy',
      crypto: selectedCrypto,
      amount,
      price,
      leverage,
      timestamp: new Date().toLocaleTimeString()
    };
    setTrades(prev => [trade, ...prev]);
    onScoreUpdate(Math.floor(amount * price * 0.1), 0);
  };

  const sellCrypto = () => {
    const currentAmount = portfolio[selectedCrypto] || 0;
    if (currentAmount < amount) {
      alert('Insufficient holdings!');
      return;
    }
    
    const price = cryptoPrices[selectedCrypto];
    const totalValue = price * amount;
    setBalance(prev => prev + totalValue);
    setPortfolio(prev => ({
      ...prev,
      [selectedCrypto]: currentAmount - amount
    }));
    
    const trade = {
      id: Date.now(),
      type: 'sell',
      crypto: selectedCrypto,
      amount,
      price,
      leverage: 1,
      timestamp: new Date().toLocaleTimeString()
    };
    setTrades(prev => [trade, ...prev]);
    onScoreUpdate(Math.floor(amount * price * 0.15), 0);
  };

  const openPosition = (posType) => {
    const price = cryptoPrices[selectedCrypto];
    const margin = (price * amount * leverage) / leverage;
    
    if (balance < margin) {
      alert('Insufficient margin!');
      return;
    }
    
    setPosition({
      type: posType,
      crypto: selectedCrypto,
      amount,
      entryPrice: price,
      leverage,
      timestamp: new Date().toLocaleTimeString()
    });
    
    setBalance(prev => prev - margin);
    const trade = {
      id: Date.now(),
      type: `${posType} position`,
      crypto: selectedCrypto,
      amount,
      price,
      leverage,
      timestamp: new Date().toLocaleTimeString()
    };
    setTrades(prev => [trade, ...prev]);
    onScoreUpdate(Math.floor(margin * 0.2), 0);
  };

  const closePosition = () => {
    if (!position) return;
    
    const currentPrice = cryptoPrices[position.crypto];
    const priceDiff = currentPrice - position.entryPrice;
    const pnl = position.type === 'long' 
      ? priceDiff * position.amount * position.leverage 
      : -priceDiff * position.amount * position.leverage;
    
    setBalance(prev => prev + (position.entryPrice * position.amount) + pnl);
    setPosition(null);
    onScoreUpdate(Math.floor(Math.abs(pnl) * 0.3), 0);
  };

  if (!isActive) return null;

  const totalPortfolioValue = Object.keys(portfolio).reduce((total, crypto) => {
    return total + (portfolio[crypto] * cryptoPrices[crypto]);
  }, balance);

  return (
    <div className="text-center">
      <div className="mb-6 grid grid-cols-1 md:grid-cols-3 gap-4">
        <div className={`p-4 rounded-lg ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
          <div className="text-sm text-gray-400">Balance</div>
          <div className="text-2xl font-bold text-green-500">${balance.toLocaleString()}</div>
        </div>
        <div className={`p-4 rounded-lg ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
          <div className="text-sm text-gray-400">Portfolio Value</div>
          <div className="text-2xl font-bold text-blue-500">${totalPortfolioValue.toLocaleString()}</div>
        </div>
        <div className={`p-4 rounded-lg ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
          <div className="text-sm text-gray-400">Game Time</div>
          <div className="text-2xl font-bold text-purple-500">{Math.floor(gameTime / 20)} min</div>
        </div>
      </div>

      <div className="mb-6">
        <h3 className={`text-lg font-bold mb-3 ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>Crypto Prices</h3>
        <div className="grid grid-cols-2 md:grid-cols-5 gap-2">
          {Object.entries(cryptoPrices).map(([crypto, price]) => (
            <div key={crypto} className={`p-3 rounded-lg ${selectedCrypto === crypto ? 'bg-yellow-500 bg-opacity-20' : isDarkMode ? 'bg-gray-700' : 'bg-gray-200'}`}>
              <div className="font-bold">{crypto}</div>
              <div className="text-sm">${price.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</div>
            </div>
          ))}
        </div>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
        <div className={`p-4 rounded-xl ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
          <h4 className="font-bold mb-3 text-center">Trade Settings</h4>
          <div className="space-y-3">
            <select
              value={selectedCrypto}
              onChange={(e) => setSelectedCrypto(e.target.value)}
              className={`w-full p-2 rounded ${isDarkMode ? 'bg-gray-700 text-white' : 'bg-white text-gray-800'}`}
            >
              {Object.keys(cryptoPrices).map(crypto => (
                <option key={crypto} value={crypto}>{crypto}</option>
              ))}
            </select>
            
            <input
              type="number"
              value={amount}
              onChange={(e) => setAmount(Math.max(0.001, parseFloat(e.target.value) || 0.001))}
              className={`w-full p-2 rounded ${isDarkMode ? 'bg-gray-700 text-white' : 'bg-white text-gray-800'}`}
              placeholder="Amount"
              step="0.001"
              min="0.001"
            />
            
            <select
              value={leverage}
              onChange={(e) => setLeverage(parseInt(e.target.value))}
              className={`w-full p-2 rounded ${isDarkMode ? 'bg-gray-700 text-white' : 'bg-white text-gray-800'}`}
            >
              <option value={1}>1x Leverage</option>
              <option value={2}>2x Leverage</option>
              <option value={5}>5x Leverage</option>
              <option value={10}>10x Leverage</option>
            </select>
          </div>
        </div>

        <div className={`p-4 rounded-xl ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
          <h4 className="font-bold mb-3 text-center">Actions</h4>
          <div className="grid grid-cols-2 gap-2">
            <button
              onClick={buyCrypto}
              className="p-2 bg-green-600 text-white rounded hover:bg-green-700 transition-colors"
            >
              Buy
            </button>
            <button
              onClick={sellCrypto}
              className="p-2 bg-red-600 text-white rounded hover:bg-red-700 transition-colors"
            >
              Sell
            </button>
            <button
              onClick={() => openPosition('long')}
              className="p-2 bg-blue-600 text-white rounded hover:bg-blue-700 transition-colors"
            >
              Long
            </button>
            <button
              onClick={() => openPosition('short')}
              className="p-2 bg-purple-600 text-white rounded hover:bg-purple-700 transition-colors"
            >
              Short
            </button>
            {position && (
              <button
                onClick={closePosition}
                className="col-span-2 p-2 bg-yellow-600 text-white rounded hover:bg-yellow-700 transition-colors"
              >
                Close Position
              </button>
            )}
          </div>
          
          {position && (
            <div className="mt-3 p-2 bg-gray-700 rounded text-sm">
              <div>Position: {position.type} {position.amount} {position.crypto}</div>
              <div>Entry: ${position.entryPrice.toLocaleString()}</div>
              <div>Leverage: {position.leverage}x</div>
            </div>
          )}
        </div>
      </div>

      <div className={`p-4 rounded-xl ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
        <h4 className="font-bold mb-3 text-center">Recent Trades</h4>
        <div className="max-h-32 overflow-y-auto">
          {trades.slice(0, 5).map(trade => (
            <div key={trade.id} className="flex justify-between text-sm py-1 border-b border-gray-600">
              <span>{trade.type} {trade.amount} {trade.crypto}</span>
              <span>${trade.price.toLocaleString()}</span>
              <span>{trade.timestamp}</span>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};

// NEW: Multiplayer Poker Room
const MultiplayerPokerGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [players, setPlayers] = useState([
    { id: 1, name: 'You', chips: 1000, cards: [], isDealer: false, isPlaying: true },
    { id: 2, name: 'Player 2', chips: 1000, cards: [], isDealer: true, isPlaying: true },
    { id: 3, name: 'Player 3', chips: 1000, cards: [], isDealer: false, isPlaying: true },
    { id: 4, name: 'Player 4', chips: 1000, cards: [], isDealer: false, isPlaying: true }
  ]);
  const [communityCards, setCommunityCards] = useState([]);
  const [pot, setPot] = useState(0);
  const [currentBet, setCurrentBet] = useState(0);
  const [currentPlayer, setCurrentPlayer] = useState(0);
  const [gamePhase, setGamePhase] = useState('pre-flop'); // pre-flop, flop, turn, river, showdown
  const [deck, setDeck] = useState([]);
  const [messages, setMessages] = useState(['Welcome to Multiplayer Poker!']);

  const createDeck = () => {
    const suits = ['♠', '♥', '♦', '♣'];
    const ranks = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A'];
    const deck = [];
    for (const suit of suits) {
      for (const rank of ranks) {
        deck.push({ suit, rank, id: `${suit}-${rank}` });
      }
    }
    return deck;
  };

  const shuffleDeck = (deck) => {
    const shuffled = [...deck];
    for (let i = shuffled.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
    }
    return shuffled;
  };

  const startNewHand = () => {
    const newDeck = shuffleDeck(createDeck());
    setDeck(newDeck);
    
    // Deal 2 cards to each player
    const newPlayers = players.map((player, index) => ({
      ...player,
      cards: [newDeck[index * 2], newDeck[index * 2 + 1]]
    }));
    
    setPlayers(newPlayers);
    setCommunityCards([]);
    setPot(20); // Small blind + big blind
    setCurrentBet(10); // Big blind
    setCurrentPlayer(2); // Player after big blind
    setGamePhase('pre-flop');
    setMessages(prev => [...prev, 'New hand started!']);
  };

  const dealFlop = () => {
    const newCommunityCards = deck.slice(8, 11);
    setCommunityCards(newCommunityCards);
    setGamePhase('flop');
    setCurrentPlayer(0);
    setMessages(prev => [...prev, 'Flop dealt!']);
  };

  const dealTurn = () => {
    const newCommunityCards = [...communityCards, deck[11]];
    setCommunityCards(newCommunityCards);
    setGamePhase('turn');
    setCurrentPlayer(0);
    setMessages(prev => [...prev, 'Turn card dealt!']);
  };

  const dealRiver = () => {
    const newCommunityCards = [...communityCards, deck[12]];
    setCommunityCards(newCommunityCards);
    setGamePhase('river');
    setCurrentPlayer(0);
    setMessages(prev => [...prev, 'River card dealt!']);
  };

  const fold = () => {
    const newPlayers = [...players];
    newPlayers[currentPlayer].isPlaying = false;
    setPlayers(newPlayers);
    const nextPlayer = (currentPlayer + 1) % players.length;
    setCurrentPlayer(nextPlayer);
    setMessages(prev => [...prev, `${players[currentPlayer].name} folded`]);
  };

  const call = () => {
    const newPlayers = [...players];
    const betAmount = currentBet - (pot / players.length); // Simplified
    newPlayers[currentPlayer].chips -= betAmount;
    setPlayers(newPlayers);
    setPot(prev => prev + betAmount);
    const nextPlayer = (currentPlayer + 1) % players.length;
    setCurrentPlayer(nextPlayer);
    setMessages(prev => [...prev, `${players[currentPlayer].name} called ${betAmount}`]);
  };

  const raise = (amount) => {
    const newPlayers = [...players];
    newPlayers[currentPlayer].chips -= amount;
    setPlayers(newPlayers);
    setPot(prev => prev + amount);
    setCurrentBet(prev => prev + amount);
    const nextPlayer = (currentPlayer + 1) % players.length;
    setCurrentPlayer(nextPlayer);
    setMessages(prev => [...prev, `${players[currentPlayer].name} raised ${amount}`]);
  };

  useEffect(() => {
    if (isActive) {
      startNewHand();
    }
  }, [isActive]);

  if (!isActive) return null;

  return (
    <div className="text-center">
      <div className="mb-6">
        <div className="text-2xl font-bold mb-2">Texas Hold'em Poker</div>
        <div className="text-lg">Pot: ${pot}</div>
        <div className="text-sm text-gray-400">Phase: {gamePhase}</div>
      </div>

      {/* Community Cards */}
      <div className="mb-6">
        <h3 className="font-bold mb-2">Community Cards</h3>
        <div className="flex justify-center gap-2">
          {communityCards.map((card, index) => (
            <div key={index} className="w-12 h-16 bg-white rounded shadow flex items-center justify-center">
              <span className="text-sm">{card.rank}{card.suit}</span>
            </div>
          ))}
          {communityCards.length === 0 && <div className="text-gray-400">No cards yet</div>}
        </div>
      </div>

      {/* Player Table */}
      <div className="grid grid-cols-2 md:grid-cols-4 gap-4 mb-6">
        {players.map((player, index) => (
          <div key={player.id} className={`p-3 rounded-lg ${currentPlayer === index ? 'ring-2 ring-yellow-400' : ''} ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
            <div className="font-bold">{player.name}</div>
            <div className="text-sm text-gray-400">Chips: ${player.chips}</div>
            {player.isDealer && <div className="text-xs bg-yellow-500 text-black px-1 rounded">Dealer</div>}
            {player.isPlaying && (
              <div className="flex gap-1 mt-2">
                {player.cards.map((card, cardIndex) => (
                  <div key={cardIndex} className="w-8 h-12 bg-white rounded shadow flex items-center justify-center text-xs">
                    {player.name === 'You' ? `${card.rank}${card.suit}` : '?'}
                  </div>
                ))}
              </div>
            )}
          </div>
        ))}
      </div>

      {/* Game Controls */}
      {players[currentPlayer]?.name === 'You' && (
        <div className="grid grid-cols-2 md:grid-cols-5 gap-2 mb-6">
          <button
            onClick={fold}
            className="p-2 bg-red-600 text-white rounded hover:bg-red-700"
          >
            Fold
          </button>
          <button
            onClick={call}
            className="p-2 bg-blue-600 text-white rounded hover:bg-blue-700"
          >
            Call
          </button>
          <button
            onClick={() => raise(20)}
            className="p-2 bg-green-600 text-white rounded hover:bg-green-700"
          >
            Raise 20
          </button>
          <button
            onClick={() => raise(50)}
            className="p-2 bg-purple-600 text-white rounded hover:bg-purple-700"
          >
            Raise 50
          </button>
          <button
            onClick={() => raise(100)}
            className="p-2 bg-yellow-600 text-white rounded hover:bg-yellow-700"
          >
            Raise 100
          </button>
        </div>
      )}

      {/* Phase Controls */}
      {players[currentPlayer]?.name !== 'You' && gamePhase === 'pre-flop' && (
        <button
          onClick={dealFlop}
          className="px-4 py-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white rounded-full font-bold"
        >
          Deal Flop
        </button>
      )}
      {players[currentPlayer]?.name !== 'You' && gamePhase === 'flop' && (
        <button
          onClick={dealTurn}
          className="px-4 py-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white rounded-full font-bold"
        >
          Deal Turn
        </button>
      )}
      {players[currentPlayer]?.name !== 'You' && gamePhase === 'turn' && (
        <button
          onClick={dealRiver}
          className="px-4 py-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white rounded-full font-bold"
        >
          Deal River
        </button>
      )}

      {/* Chat/Messages */}
      <div className={`p-3 rounded-lg max-h-32 overflow-y-auto ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
        {messages.slice(-5).map((msg, index) => (
          <div key={index} className="text-sm py-1">{msg}</div>
        ))}
      </div>
    </div>
  );
};

// NEW: Stock Market Simulator
const StockMarketGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [balance, setBalance] = useState(50000);
  const [portfolio, setPortfolio] = useState({});
  const [stockPrices, setStockPrices] = useState({
    AAPL: 175.50,
    GOOGL: 142.30,
    MSFT: 338.11,
    TSLA: 248.50,
    AMZN: 145.86,
    META: 325.78,
    NVDA: 485.09
  });
  const [selectedStock, setSelectedStock] = useState('AAPL');
  const [shares, setShares] = useState(10);
  const [watchlist, setWatchlist] = useState(['AAPL', 'TSLA', 'NVDA']);
  const [orders, setOrders] = useState([]);

  // Simulate stock price movements
  useEffect(() => {
    if (!isActive) return;
    
    const interval = setInterval(() => {
      setStockPrices(prev => {
        const newPrices = {};
        Object.keys(prev).forEach(stock => {
          const change = (Math.random() - 0.5) * 0.03; // -1.5% to +1.5%
          newPrices[stock] = prev[stock] * (1 + change);
        });
        return newPrices;
      });
    }, 5000);

    return () => clearInterval(interval);
  }, [isActive]);

  const buyStock = () => {
    const price = stockPrices[selectedStock];
    const totalCost = price * shares;
    
    if (balance < totalCost) {
      alert('Insufficient funds!');
      return;
    }
    
    setBalance(prev => prev - totalCost);
    setPortfolio(prev => ({
      ...prev,
      [selectedStock]: (prev[selectedStock] || 0) + shares
    }));
    
    const order = {
      id: Date.now(),
      type: 'buy',
      symbol: selectedStock,
      shares,
      price,
      timestamp: new Date().toLocaleTimeString()
    };
    setOrders(prev => [order, ...prev]);
    onScoreUpdate(Math.floor(totalCost * 0.05), 0);
  };

  const sellStock = () => {
    const currentShares = portfolio[selectedStock] || 0;
    if (currentShares < shares) {
      alert('Insufficient shares!');
      return;
    }
    
    const price = stockPrices[selectedStock];
    const totalValue = price * shares;
    setBalance(prev => prev + totalValue);
    setPortfolio(prev => ({
      ...prev,
      [selectedStock]: currentShares - shares
    }));
    
    const order = {
      id: Date.now(),
      type: 'sell',
      symbol: selectedStock,
      shares,
      price,
      timestamp: new Date().toLocaleTimeString()
    };
    setOrders(prev => [order, ...prev]);
    onScoreUpdate(Math.floor(totalValue * 0.07), 0);
  };

  const addToWatchlist = (symbol) => {
    if (!watchlist.includes(symbol)) {
      setWatchlist(prev => [...prev, symbol]);
    }
  };

  const removeFromWatchlist = (symbol) => {
    setWatchlist(prev => prev.filter(s => s !== symbol));
  };

  if (!isActive) return null;

  const totalPortfolioValue = Object.keys(portfolio).reduce((total, symbol) => {
    return total + (portfolio[symbol] * stockPrices[symbol]);
  }, balance);

  return (
    <div className="text-center">
      <div className="mb-6 grid grid-cols-1 md:grid-cols-3 gap-4">
        <div className={`p-4 rounded-lg ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
          <div className="text-sm text-gray-400">Cash Balance</div>
          <div className="text-2xl font-bold text-green-500">${balance.toLocaleString()}</div>
        </div>
        <div className={`p-4 rounded-lg ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
          <div className="text-sm text-gray-400">Portfolio Value</div>
          <div className="text-2xl font-bold text-blue-500">${totalPortfolioValue.toLocaleString()}</div>
        </div>
        <div className={`p-4 rounded-lg ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
          <div className="text-sm text-gray-400">Total Return</div>
          <div className={`text-2xl font-bold ${totalPortfolioValue >= 50000 ? 'text-green-500' : 'text-red-500'}`}>
            {((totalPortfolioValue - 50000) / 50000 * 100).toFixed(2)}%
          </div>
        </div>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
        {/* Watchlist */}
        <div className={`p-4 rounded-xl ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
          <h4 className="font-bold mb-3 text-center">Watchlist</h4>
          <div className="space-y-2 max-h-48 overflow-y-auto">
            {watchlist.map(symbol => (
              <div key={symbol} className="flex justify-between items-center p-2 bg-gray-700 rounded">
                <div>
                  <div className="font-bold">{symbol}</div>
                  <div className="text-sm">${stockPrices[symbol]?.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</div>
                </div>
                <button
                  onClick={() => removeFromWatchlist(symbol)}
                  className="text-red-400 hover:text-red-300"
                >
                  Remove
                </button>
              </div>
            ))}
          </div>
          
          <div className="mt-3">
            <select
              value={selectedStock}
              onChange={(e) => setSelectedStock(e.target.value)}
              className={`w-full p-2 rounded mb-2 ${isDarkMode ? 'bg-gray-700 text-white' : 'bg-white text-gray-800'}`}
            >
              {Object.keys(stockPrices).map(symbol => (
                <option key={symbol} value={symbol}>{symbol}</option>
              ))}
            </select>
            <button
              onClick={() => addToWatchlist(selectedStock)}
              disabled={watchlist.includes(selectedStock)}
              className="w-full p-2 bg-blue-600 text-white rounded disabled:bg-gray-500"
            >
              Add to Watchlist
            </button>
          </div>
        </div>

        {/* Trading Panel */}
        <div className={`p-4 rounded-xl ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
          <h4 className="font-bold mb-3 text-center">Trade</h4>
          <div className="space-y-3">
            <div>
              <label className="block text-sm mb-1">Shares</label>
              <input
                type="number"
                value={shares}
                onChange={(e) => setShares(Math.max(1, parseInt(e.target.value) || 1))}
                className={`w-full p-2 rounded ${isDarkMode ? 'bg-gray-700 text-white' : 'bg-white text-gray-800'}`}
                min="1"
              />
            </div>
            
            <div className="grid grid-cols-2 gap-2">
              <button
                onClick={buyStock}
                className="p-3 bg-green-600 text-white rounded hover:bg-green-700 transition-colors"
              >
                <div className="font-bold">Buy</div>
                <div className="text-xs">${(stockPrices[selectedStock] * shares).toLocaleString()}</div>
              </button>
              <button
                onClick={sellStock}
                className="p-3 bg-red-600 text-white rounded hover:bg-red-700 transition-colors"
              >
                <div className="font-bold">Sell</div>
                <div className="text-xs">${(stockPrices[selectedStock] * shares).toLocaleString()}</div>
              </button>
            </div>
          </div>
        </div>
      </div>

      {/* Market Overview */}
      <div className={`p-4 rounded-xl ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
        <h4 className="font-bold mb-3 text-center">Market Overview</h4>
        <div className="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-7 gap-2">
          {Object.entries(stockPrices).map(([symbol, price]) => (
            <div key={symbol} className={`p-2 rounded text-center ${isDarkMode ? 'bg-gray-700' : 'bg-gray-200'}`}>
              <div className="font-bold text-sm">{symbol}</div>
              <div className="text-xs">${price.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</div>
              <div className={`text-xs ${Math.random() > 0.5 ? 'text-green-500' : 'text-red-500'}`}>
                {Math.random() > 0.5 ? <ArrowUpRight size={12} /> : <ArrowDownRight size={12} />}
                {(Math.random() * 5).toFixed(2)}%
              </div>
            </div>
          ))}
        </div>
      </div>

      {/* Order History */}
      <div className={`p-4 rounded-xl mt-4 ${isDarkMode ? 'bg-gray-800' : 'bg-gray-100'}`}>
        <h4 className="font-bold mb-3 text-center">Recent Orders</h4>
        <div className="max-h-32 overflow-y-auto">
          {orders.slice(0, 5).map(order => (
            <div key={order.id} className="flex justify-between text-sm py-1 border-b border-gray-600">
              <span className={order.type === 'buy' ? 'text-green-500' : 'text-red-500'}>
                {order.type.toUpperCase()} {order.shares} {order.symbol}
              </span>
              <span>${order.price.toLocaleString()}</span>
              <span>{order.timestamp}</span>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};

// Main Game Component
const CardGame = ({ isActive, onScoreUpdate, isDarkMode }) => {
  const [deck, setDeck] = useState([]);
  const [playerHand, setPlayerHand] = useState([]);
  const [computerHand, setComputerHand] = useState([]);
  const [playerScore, setPlayerScore] = useState(0);
  const [computerScore, setComputerScore] = useState(0);
  const [selectedCard, setSelectedCard] = useState(null);
  const [gameStarted, setGameStarted] = useState(false);
  const [gameOver, setGameOver] = useState(false);
  const [winner, setWinner] = useState('');

  const initializeGame = () => {
    const newDeck = shuffleDeck(createDeck());
    setDeck(newDeck);
    setPlayerHand(newDeck.slice(0, 5));
    setComputerHand(newDeck.slice(5, 10));
    setPlayerScore(0);
    setComputerScore(0);
    setSelectedCard(null);
    setGameStarted(true);
    setGameOver(false);
    setWinner('');
  };

  const handlePlayCard = () => {
    if (!selectedCard || gameOver) return;

    const newPlayerHand = playerHand.filter(card => card.id !== selectedCard.id);
    setPlayerHand(newPlayerHand);
    const cardValue = getCardValue(selectedCard);
    const newPlayerScore = playerScore + cardValue;
    setPlayerScore(newPlayerScore);
    setSelectedCard(null);

    if (computerHand.length > 0) {
      const randomIndex = Math.floor(Math.random() * computerHand.length);
      const computerCard = computerHand[randomIndex];
      const newComputerHand = [...computerHand];
      newComputerHand.splice(randomIndex, 1);
      setComputerHand(newComputerHand);
      const computerCardValue = getCardValue(computerCard);
      const newComputerScore = computerScore + computerCardValue;
      setComputerScore(newComputerScore);
    }

    if (newPlayerHand.length === 0 || newPlayerScore >= 50) {
      setGameOver(true);
      setWinner('Player');
      onScoreUpdate(newPlayerScore, 0);
    } else if (computerHand.length === 0 || computerScore >= 50) {
      setGameOver(true);
      setWinner('Computer');
      onScoreUpdate(newPlayerScore, 0);
    }
  };

  const handleSkipTurn = () => {
    if (gameOver) return;
    if (computerHand.length > 0) {
      const randomIndex = Math.floor(Math.random() * computerHand.length);
      const computerCard = computerHand[randomIndex];
      const newComputerHand = [...computerHand];
      newComputerHand.splice(randomIndex, 1);
      setComputerHand(newComputerHand);
      const computerCardValue = getCardValue(computerCard);
      const newComputerScore = computerScore + computerCardValue;
      setComputerScore(newComputerScore);
      
      if (computerScore >= 50) {
        setGameOver(true);
        setWinner('Computer');
        onScoreUpdate(playerScore, 0);
      }
    }
  };

  useEffect(() => {
    if (isActive) {
      initializeGame();
    }
  }, [isActive]);

  if (!isActive) return null;

  return (
    <div>
      <div className="mb-4 flex justify-center gap-4">
        <div className="px-4 py-2 bg-blue-600 text-white rounded-full">Your Score: {playerScore}</div>
        <div className="px-4 py-2 bg-red-600 text-white rounded-full">Computer: {computerScore}</div>
      </div>

      <div className="mb-6">
        <h3 className={`text-center mb-2 ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>Computer's Hand</h3>
        <div className="flex justify-center gap-1">
          {computerHand.map((_, index) => (
            <CardComponent key={index} isFlipped={true} />
          ))}
        </div>
      </div>

      <div className="mb-6">
        <h3 className={`text-center mb-2 ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>Your Hand</h3>
        <div className="flex justify-center gap-2">
          {playerHand.map((card) => (
            <CardComponent
              key={card.id}
              card={card}
              isHighlighted={selectedCard?.id === card.id}
              onClick={() => setSelectedCard(card)}
            />
          ))}
        </div>
      </div>

      <div className="flex justify-center gap-3">
        <button
          onClick={handlePlayCard}
          disabled={!selectedCard || gameOver}
          className="px-4 py-2 bg-gradient-to-r from-blue-500 to-indigo-600 text-white rounded-full font-bold shadow-lg hover:from-blue-600 hover:to-indigo-700 transform hover:scale-105 transition-all duration-200 disabled:opacity-50"
        >
          Play Card
        </button>
        <button
          onClick={handleSkipTurn}
          disabled={gameOver}
          className="px-4 py-2 bg-gradient-to-r from-orange-500 to-red-600 text-white rounded-full font-bold shadow-lg hover:from-orange-600 hover:to-red-700 transform hover:scale-105 transition-all duration-200 disabled:opacity-50"
        >
          Skip Turn
        </button>
        <button
          onClick={initializeGame}
          className="px-4 py-2 bg-gradient-to-r from-gray-500 to-gray-600 text-white rounded-full font-bold shadow-lg hover:from-gray-600 hover:to-gray-700 transform hover:scale-105 transition-all duration-200"
        >
          New Game
        </button>
      </div>

      {gameOver && (
        <div className="text-center mt-4">
          <p className={`text-xl font-bold ${winner === 'Player' ? 'text-green-600' : 'text-red-600'}`}>
            {winner} wins!
          </p>
        </div>
      )}
    </div>
  );
};

const GameCard = ({ title, description, icon: Icon, onClick, isActive, isDarkMode }) => (
  <div 
    className={`p-4 rounded-xl cursor-pointer transform transition-all duration-300 hover:scale-105 ${
      isActive 
        ? 'bg-gradient-to-br from-yellow-400 to-orange-500 shadow-2xl ring-4 ring-yellow-300' 
        : isDarkMode 
          ? 'bg-gradient-to-br from-purple-700 to-blue-800 hover:from-purple-800 hover:to-blue-900 shadow-xl'
          : 'bg-gradient-to-br from-purple-200 to-blue-300 hover:from-purple-300 hover:to-blue-400 shadow-xl'
    }`}
    onClick={onClick}
  >
    <div className="flex flex-col items-center text-center">
      <Icon size={32} className="text-white mb-2" />
      <h3 className="text-lg font-bold text-white mb-1">{title}</h3>
      <p className={isDarkMode ? "text-purple-100 text-xs" : "text-purple-700 text-xs"}>{description}</p>
    </div>
  </div>
);

const ScoreDisplay = ({ score, label, icon: Icon, color, isDarkMode }) => (
  <div className={`flex items-center gap-2 px-4 py-2 rounded-full bg-gradient-to-r ${color} text-white shadow-lg`}>
    <Icon size={20} />
    <span className="font-bold">{label}: {score}</span>
  </div>
);

export default function App() {
  const [activeGame, setActiveGame] = useState('card');
  const [totalScore, setTotalScore] = useState(0);
  const [gameScores, setGameScores] = useState({
    card: 0,
    dice: 0,
    memory: 0,
    target: 0,
    roulette: 0,
    rps: 0,
    number: 0,
    tictactoe: 0,
    whack: 0,
    wordle: 0,
    chat: 0,
    crypto: 0,
    poker: 0,
    stocks: 0,
    social: 0
  });
  const [showShareModal, setShowShareModal] = useState(false);
  const [isDarkMode, setIsDarkMode] = useState(true);

  const toggleTheme = () => {
    setIsDarkMode(!isDarkMode);
  };

  const handleScoreUpdate = (score, bonus) => {
    const newScore = score + bonus;
    setGameScores(prev => ({ ...prev, [activeGame]: newScore }));
    setTotalScore(prev => prev + newScore);
  };

  const games = [
    {
      id: 'card',
      title: 'Card Challenge',
      description: 'Strategic card game',
      icon: Gamepad2,
      component: CardGame
    },
    {
      id: 'dice',
      title: 'Lucky Dice',
      description: 'Roll and score points',
      icon: Dice5,
      component: DiceGame
    },
    {
      id: 'memory',
      title: 'Memory Match',
      description: 'Match emoji pairs',
      icon: Puzzle,
      component: MemoryGame
    },
    {
      id: 'target',
      title: 'Target Practice',
      description: 'Shoot for points',
      icon: Target,
      component: TargetGame
    },
    {
      id: 'roulette',
      title: 'Roulette Spin',
      description: 'Classic casino game',
      icon: Circle,
      component: RouletteGame
    },
    {
      id: 'rps',
      title: 'Rock Paper Scissors',
      description: 'Best of 5 rounds',
      icon: Square,
      component: RockPaperScissorsGame
    },
    {
      id: 'number',
      title: 'Number Guess',
      description: 'Guess the secret number',
      icon: Hash,
      component: NumberGuessingGame
    },
    {
      id: 'tictactoe',
      title: 'Tic Tac Toe',
      description: 'Classic X and O game',
      icon: Star,
      component: TicTacToeGame
    },
    {
      id: 'whack',
      title: 'Whack-a-Mole',
      description: '30-second challenge',
      icon: Triangle,
      component: WhackAMoleGame
    },
    {
      id: 'wordle',
      title: 'Word Puzzle',
      description: 'Guess the 5-letter word',
      icon: MessageSquare,
      component: WordleGame
    },
    {
      id: 'chat',
      title: 'Bilpcoin Fun Chat',
      description: 'Share and connect with players',
      icon: Users,
      component: BilpcoinFunChat
    },
    {
      id: 'crypto',
      title: 'Crypto Trading',
      description: 'Trade crypto with leverage',
      icon: Bitcoin,
      component: CryptoTradingGame
    },
    {
      id: 'poker',
      title: 'Multiplayer Poker',
      description: 'Texas Hold\'em with friends',
      icon: Users2,
      component: MultiplayerPokerGame
    },
    {
      id: 'stocks',
      title: 'Stock Market',
      description: 'Invest in real companies',
      icon: TrendingUp,
      component: StockMarketGame
    },
    {
      id: 'social',
      title: 'Bilpcoin Social',
      description: 'Enhanced social networking platform',
      icon: Network,
      component: BilpcoinSocial
    }
  ];

  const GameComponent = games.find(game => game.id === activeGame)?.component;

  return (
    <div className={`min-h-screen relative ${isDarkMode ? '' : 'bg-gradient-to-br from-gray-50 to-gray-100'}`}>
      <FunBackground isDarkMode={isDarkMode} />
      <div className="relative z-10 p-2">
        <div className="max-w-7xl mx-auto">
          {/* Header with Theme Toggle */}
          <div className="text-center mb-6 relative">
            <div className="absolute -top-4 -left-4 w-12 h-12 bg-yellow-400 rounded-full flex items-center justify-center text-2xl animate-bounce">
              ₿
            </div>
            <div className="absolute -top-4 -right-4 w-12 h-12 bg-red-500 rounded-full flex items-center justify-center text-2xl animate-pulse">
              💰
            </div>
            
            {/* Theme Toggle Button */}
            <button
              onClick={toggleTheme}
              className={`absolute top-0 right-0 p-2 rounded-full ${
                isDarkMode 
                  ? 'bg-gray-700 text-yellow-300 hover:bg-gray-600' 
                  : 'bg-yellow-300 text-gray-800 hover:bg-yellow-400'
              } transition-all duration-200`}
            >
              {isDarkMode ? <Sun size={20} /> : <Moon size={20} />}
            </button>
            
            <h1 className={`text-5xl font-bold mb-2 bg-gradient-to-r from-yellow-400 to-orange-500 bg-clip-text text-transparent relative z-10 ${
              isDarkMode ? 'text-transparent' : ''
            }`}>
              Bilpcoin Fun
            </h1>
            <p className={isDarkMode ? "text-purple-200" : "text-purple-600"}>Fifteen exciting games plus enhanced social features!</p>
          </div>

          {/* Total Score with Share Button */}
          <div className="text-center mb-6 flex justify-center items-center gap-4">
            <ScoreDisplay 
              score={totalScore} 
              label="Total Score" 
              icon={Award} 
              color="from-yellow-500 to-orange-600"
              isDarkMode={isDarkMode}
            />
            <button
              onClick={() => setShowShareModal(true)}
              className="flex items-center gap-2 px-4 py-2 bg-gradient-to-r from-purple-600 to-pink-600 text-white rounded-full font-bold shadow-lg hover:from-purple-700 hover:to-pink-700 transform hover:scale-105 transition-all duration-200"
            >
              <Share2 size={18} />
              Share
            </button>
          </div>

          {/* Game Selection */}
          <div className="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-7 gap-3 mb-6">
            {games.map((game) => (
              <GameCard
                key={game.id}
                title={game.title}
                description={game.description}
                icon={game.icon}
                onClick={() => setActiveGame(game.id)}
                isActive={activeGame === game.id}
                isDarkMode={isDarkMode}
              />
            ))}
          </div>

          {/* Active Game */}
          <div className={`${isDarkMode ? 'bg-black bg-opacity-30' : 'bg-white bg-opacity-70'} rounded-2xl p-4 backdrop-blur-sm min-h-80 border border-yellow-400 border-opacity-20`}>
            {GameComponent && <GameComponent 
              isActive={true} 
              onScoreUpdate={(activeGame !== 'chat' && activeGame !== 'social') ? handleScoreUpdate : () => {}}
              isDarkMode={isDarkMode}
            />}
          </div>

          {/* Game Scores */}
          {activeGame !== 'chat' && activeGame !== 'social' && (
            <div className={`mt-6 rounded-xl p-4 backdrop-blur-sm border border-purple-500 border-opacity-20 ${
              isDarkMode ? 'bg-black bg-opacity-30' : 'bg-white bg-opacity-50'
            }`}>
              <h3 className={`text-xl font-bold mb-3 text-center ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>Game Scores</h3>
              <div className="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 lg:grid-cols-7 gap-3">
                {games.filter(g => g.id !== 'chat' && g.id !== 'social').map((game) => (
                  <div key={game.id} className="text-center">
                    <div className={`font-semibold text-xs ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>{game.title}</div>
                    <div className="text-yellow-500 font-bold text-sm">{gameScores[game.id]}</div>
                  </div>
                ))}
              </div>
            </div>
          )}
        </div>
      </div>
      
      <ShareModal 
        isOpen={showShareModal} 
        onClose={() => setShowShareModal(false)} 
        totalScore={totalScore}
        isDarkMode={isDarkMode}
      />
    </div>
  );
}
