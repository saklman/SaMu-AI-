import React, { useState, useEffect } from 'react';
import { MessageCircle, Plus, Search, Menu, X, Save, Mic, Calendar, Lock, Heart, Sparkles, ArrowLeft, Send } from 'lucide-react';

const SaMuDiary = () => {
const [currentView, setCurrentView] = useState('home');
const [entries, setEntries] = useState([
{
id: 1,
title: "1 day",
date: "June 24, 2025 00:29",
content: "To day I was goto university, and meat with sir Razaq shar",
mood: "😊",
category: "daily"
},
{
id: 2,
title: "A New Beginning",
date: "June 22, 2025 00:28",
content: "Today feels different. Like the start of a new chapter. I feel a sense of calm optimism I haven't felt in a while. The city was quiet this morning, and the coffee tasted especially good.",
mood: "😊",
category: "feelings"
},
{
id: 3,
title: "The Remini Premium Mod",
date: "May 15, 2024 23:30",
content: "Spent the whole afternoon figuring out that Remini Premium mod scene. The APK bypass was tricky, but I finally cracked it. Felt like a real hacker, haha. A small victory, but a victory nonetheless.",
mood: "💡",
category: "tech"
},
{
id: 4,
title: "A Lingering Feeling",
date: "June 13, 2024 02:00",
content: "It's been a while, but some days... some days I still think about it. It feels like a weight I can't quite shake off. It's frustrating. I thought I was over it, but I guess some things just stick with you.",
mood: "😢",
category: "personal"
}
]);

const [newEntry, setNewEntry] = useState({
title: '',
content: '',
mood: '😊',
category: 'daily'
});

const [chatMessages, setChatMessages] = useState([
{ type: 'bot', text: 'Yaar Sir Salman, main tumhare saare memories yaad rakhta hun. Kuch bhi poochna hai?' }
]);
const [chatInput, setChatInput] = useState('');
const [isRecording, setIsRecording] = useState(false);

const moods = ['😊', '😢', '😡', '💡', '❤️', '😴', '🤔', '🎉'];
const categories = ['daily', 'feelings', 'tech', 'personal', 'memories'];

const handleSaveEntry = () => {
if (newEntry.title.trim() && newEntry.content.trim()) {
const entry = {
id: Date.now(),
title: newEntry.title,
date: new Date().toLocaleString('en-US', {
month: 'long',
day: 'numeric',
year: 'numeric',
hour: '2-digit',
minute: '2-digit'
}),
content: newEntry.content,
mood: newEntry.mood,
category: newEntry.category
};

setEntries([entry, ...entries]);  
  setNewEntry({ title: '', content: '', mood: '😊', category: 'daily' });  
  setCurrentView('home');  
}

};

const handleChatSend = () => {
if (chatInput.trim()) {
setChatMessages([...chatMessages,
{ type: 'user', text: chatInput },
{ type: 'bot', text: getBotResponse(chatInput) }
]);
setChatInput('');
}
};

const getBotResponse = (input) => {
const lower = input.toLowerCase();

if (lower.includes('kal') || lower.includes('yesterday')) {  
  return 'Sir Salman, kal tu likha tha: "A New Beginning" - tu keh raha tha ke tu calm aur optimistic feel kar raha hai. Coffee bhi achi thi na? 😊';  
}  
if (lower.includes('sad') || lower.includes('feeling')) {  
  return 'Yaar, June 13 ko tu bahut sad tha. Likha tha ke kuch weight hai jo shake off nahi ho raha. Main samajh sakta hun, kabhi kabhi purane wounds time lagta hai heal hone mein. 💙';  
}  
if (lower.includes('remini') || lower.includes('mod') || lower.includes('apk')) {  
  return 'Haha! May 15 ko tu Remini Premium mod crack kar raha tha. Bola tha ke real hacker jaisa feel kiya. Small victory but victory nonetheless, right? 💡';  
}  
if (lower.includes('university') || lower.includes('sir razaq')) {  
  return 'Aaj tu university gaya tha na? Sir Razaq se milne. Kya scene tha wahan? New beginning wala vibe continue hai? 🎓';  
}  
  
return 'Sir Salman, main tumhare saare entries yaad rakhta hun. Koi specific date, mood, ya topic ke baare mein poochna hai? Main sab kuch bata sakta hun! 🤖';

};

const EntryCard = ({ entry }) => (
<div className="bg-gradient-to-r from-amber-900/20 to-yellow-900/20 rounded-xl p-4 mb-4 border border-amber-700/30 backdrop-blur-sm">
<div className="flex justify-between items-start mb-2">
<h3 className="text-amber-100 font-semibold text-lg">{entry.title}</h3>
<span className="text-2xl">{entry.mood}</span>
</div>
<p className="text-amber-200/70 text-sm mb-2">{entry.date}</p>
<p className="text-amber-100/90 text-sm line-clamp-2">{entry.content}</p>
<div className="mt-2">
<span className="text-xs bg-amber-800/30 text-amber-200 px-2 py-1 rounded-full">
{entry.category}
</span>
</div>
</div>
);

return (
<div className="min-h-screen bg-gradient-to-br from-amber-950 via-yellow-900 to-amber-900 text-amber-100">
{/* Header */}
<div className="bg-gradient-to-r from-amber-900/40 to-yellow-800/40 backdrop-blur-md border-b border-amber-700/30 p-4">
<div className="flex items-center justify-between">
<div className="flex items-center space-x-3">
{currentView !== 'home' && (
<button
onClick={() => setCurrentView('home')}
className="text-amber-200 hover:text-amber-100 transition-colors"
>
<ArrowLeft size={24} />
</button>
)}
<div className="flex items-center space-x-2">
<Heart className="text-amber-400" size={24} />
<div>
<h1 className="text-xl font-bold text-amber-100">SaMu Diary</h1>
<p className="text-xs text-amber-300">Welcome back, Sir Salman.</p>
</div>
</div>
</div>

<div className="flex items-center space-x-3">  
        {currentView === 'home' && (  
          <>  
            <button   
              onClick={() => setCurrentView('chat')}  
              className="p-2 bg-amber-800/30 rounded-full hover:bg-amber-700/40 transition-colors"  
            >  
              <MessageCircle size={20} />  
            </button>  
            <button className="p-2 bg-amber-800/30 rounded-full hover:bg-amber-700/40 transition-colors">  
              <Search size={20} />  
            </button>  
          </>  
        )}  
      </div>  
    </div>  
  </div>  

  {/* Home View */}  
  {currentView === 'home' && (  
    <div className="p-4 pb-20">  
      <div className="mb-6">  
        <h2 className="text-2xl font-bold text-amber-100 mb-2 flex items-center">  
          <Sparkles className="mr-2 text-amber-400" size={24} />  
          Your Emotional Journey  
        </h2>  
        <p className="text-amber-300 text-sm">  
          {entries.length} memories captured • Your digital companion remembers everything  
        </p>  
      </div>  

      <div className="space-y-4">  
        {entries.map(entry => (  
          <EntryCard key={entry.id} entry={entry} />  
        ))}  
      </div>  

      {/* Floating Action Button */}  
      <button  
        onClick={() => setCurrentView('newEntry')}  
        className="fixed bottom-6 right-6 bg-gradient-to-r from-amber-600 to-yellow-600 p-4 rounded-full shadow-lg hover:from-amber-500 hover:to-yellow-500 transition-all transform hover:scale-105"  
      >  
        <Plus size={28} className="text-white" />  
      </button>  
    </div>  
  )}  

  {/* New Entry View */}  
  {currentView === 'newEntry' && (  
    <div className="p-4">  
      <div className="mb-6">  
        <h2 className="text-2xl font-bold text-amber-100 mb-2">New Entry</h2>  
        <p className="text-amber-300 text-sm">Capture your thoughts, feelings, and ideas.</p>  
      </div>  

      <div className="space-y-4">  
        <div>  
          <label className="block text-amber-200 text-sm font-medium mb-2">Title</label>  
          <input  
            type="text"  
            value={newEntry.title}  
            onChange={(e) => setNewEntry({...newEntry, title: e.target.value})}  
            placeholder="What's on your mind?"  
            className="w-full bg-amber-900/30 border border-amber-700/50 rounded-lg px-4 py-3 text-amber-100 placeholder-amber-400 focus:border-amber-500 focus:outline-none"  
          />  
        </div>  

        <div>  
          <label className="block text-amber-200 text-sm font-medium mb-2">Entry</label>  
          <textarea  
            value={newEntry.content}  
            onChange={(e) => setNewEntry({...newEntry, content: e.target.value})}  
            placeholder="Tell me everything..."  
            rows={8}  
            className="w-full bg-amber-900/30 border border-amber-700/50 rounded-lg px-4 py-3 text-amber-100 placeholder-amber-400 focus:border-amber-500 focus:outline-none resize-none"  
          />  
        </div>  

        <div className="flex space-x-4">  
          <div className="flex-1">  
            <label className="block text-amber-200 text-sm font-medium mb-2">Mood</label>  
            <div className="flex space-x-2">  
              {moods.map(mood => (  
                <button  
                  key={mood}  
                  onClick={() => setNewEntry({...newEntry, mood})}  
                  className={`p-2 rounded-lg text-2xl transition-all ${  
                    newEntry.mood === mood   
                      ? 'bg-amber-600/50 border-2 border-amber-400'   
                      : 'bg-amber-900/30 border border-amber-700/50 hover:bg-amber-800/40'  
                  }`}  
                >  
                  {mood}  
                </button>  
              ))}  
            </div>  
          </div>  
        </div>  

        <div className="flex space-x-3 pt-4">  
          <button  
            onClick={handleSaveEntry}  
            className="flex-1 bg-gradient-to-r from-amber-600 to-yellow-600 text-white py-3 rounded-lg font-medium hover:from-amber-500 hover:to-yellow-500 transition-all flex items-center justify-center space-x-2"  
          >  
            <Save size={20} />  
            <span>Save Entry</span>  
          </button>  
            
          <button  
            onClick={() => setIsRecording(!isRecording)}  
            className={`px-4 py-3 rounded-lg transition-all ${  
              isRecording   
                ? 'bg-red-600 hover:bg-red-500'   
                : 'bg-amber-800/30 hover:bg-amber-700/40'  
            }`}  
          >  
            <Mic size={20} />  
          </button>  
        </div>  
      </div>  
    </div>  
  )}  

  {/* Chat View */}  
  {currentView === 'chat' && (  
    <div className="flex flex-col h-screen">  
      <div className="flex-1 p-4 overflow-y-auto">  
        <div className="mb-4 text-center">  
          <h2 className="text-xl font-bold text-amber-100 mb-1">Talk with SaMu</h2>  
          <p className="text-amber-300 text-sm">Ask me anything about your past entries. I remember everything.</p>  
        </div>  

        <div className="space-y-4">  
          {chatMessages.map((msg, idx) => (  
            <div key={idx} className={`flex ${msg.type === 'user' ? 'justify-end' : 'justify-start'}`}>  
              <div className={`max-w-xs p-3 rounded-2xl ${  
                msg.type === 'user'   
                  ? 'bg-amber-600 text-white'   
                  : 'bg-amber-900/40 text-amber-100 border border-amber-700/30'  
              }`}>  
                <p className="text-sm">{msg.text}</p>  
              </div>  
            </div>  
          ))}  
        </div>  
      </div>  

      <div className="p-4 bg-gradient-to-r from-amber-900/40 to-yellow-800/40 backdrop-blur-md border-t border-amber-700/30">  
        <div className="flex space-x-3">  
          <input  
            type="text"  
            value={chatInput}  
            onChange={(e) => setChatInput(e.target.value)}  
            onKeyPress={(e) => e.key === 'Enter' && handleChatSend()}  
            placeholder="Ask about a memory or feeling..."  
            className="flex-1 bg-amber-900/30 border border-amber-700/50 rounded-full px-4 py-3 text-amber-100 placeholder-amber-400 focus:border-amber-500 focus:outline-none"  
          />  
          <button  
            onClick={handleChatSend}  
            className="bg-gradient-to-r from-amber-600 to-yellow-600 p-3 rounded-full hover:from-amber-500 hover:to-yellow-500 transition-all"  
          >  
            <Send size={20} className="text-white" />  
          </button>  
        </div>  
      </div>  
    </div>  
  )}  
</div>

);
};

export default SaMuDiary;

