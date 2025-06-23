# Jobs
Job search
import React from 'react';
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';
import { Button } from '@/components/ui/button';
import { Card, CardContent } from '@/components/ui/card';
import { Input } from '@/components/ui/input';
import { Textarea } from '@/components/ui/textarea';
import { AdSlot } from '@/components/adsense';

// Layout component with nav and AdSense placeholder
export function Layout({ children }: { children: React.ReactNode }) {
  return (
    <div className="min-h-screen flex flex-col">
      <header className="bg-white shadow p-4">
        <nav className="container mx-auto flex space-x-4">
          <Link to="/" className="font-bold">Home</Link>
          <Link to="/jobs">Jobs</Link>
          <Link to="/interviews">Interviews</Link>
          <Link to="/blog">Blog</Link>
          <Link to="/templates">Templates</Link>
          <Link to="/account">Account</Link>
        </nav>
      </header>
      <main className="flex-1 container mx-auto p-4">{children}</main>
      <footer className="bg-gray-100 p-4 text-center">
        <AdSlot adClient="ca-pub-XXXXXXXXXXXX" adSlot="YYYYYYYYYY" />
        <p className="mt-4">© 2025 JobPortal SA</p>
      </footer>
    </div>
  );
}

// Home page
export function Home() {
  return (
    <Layout>
      <h1 className="text-2xl font-bold">Welcome to JobPortal SA</h1>
      <p>Your hub for South African job opportunities, interview prep, blogs, and CV templates.</p>
    </Layout>
  );
}

// Jobs page
export function Jobs() {
  const industries = ["Finance", "IT", "Engineering", "Healthcare"];
  const provinces = ["Gauteng", "Western Cape", "KwaZulu-Natal", "Limpopo"];
  return (
    <Layout>
      <h1 className="text-xl font-semibold">Jobs by Industry & Province</h1>
      {industries.map(ind => (
        <Card key={ind} className="mb-4">
          <CardContent>
            <h2 className="font-bold">{ind}</h2>
            <ul className="list-disc ml-5">
              {provinces.map(prov => (
                <li key={prov}>
                  <a href={`https://www.examplejobs.co.za/${ind}/${prov}`} target="_blank" rel="noopener noreferrer">
                    {ind} jobs in {prov}
                  </a>
                </li>
              ))}
            </ul>
          </CardContent>
        </Card>
      ))}
    </Layout>
  );
}

// Interview preparation page
export function Interviews() {
  return (
    <Layout>
      <h1 className="text-xl font-semibold">Interview Preparation Videos</h1>
      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        <iframe
          src="https://www.youtube.com/embed/dQw4w9WgXcQ" 
          title="Interview Tips"
          className="w-full h-64"
        />
        <iframe
          src="https://www.youtube.com/embed/oHg5SJYRHA0" 
          title="Resume and Interview"
          className="w-full h-64"
        />
      </div>
    </Layout>
  );
}

// Blog page
export function Blog() {
  const posts = [
    { id: 1, title: 'Top 10 Interview Questions', summary: 'How to answer the most common interview questions.' },
    { id: 2, title: 'Handling Difficult Interviewers', summary: 'Strategies to stay calm and confident.' },
  ];
  return (
    <Layout>
      <h1 className="text-xl font-semibold">Blog: Interview Q&A</h1>
      {posts.map(p => (
        <Card key={p.id} className="mb-4">
          <CardContent>
            <h2 className="font-bold">{p.title}</h2>
            <p>{p.summary}</p>
            <Link to={`/blog/${p.id}`} className="text-blue-600">Read more →</Link>
          </CardContent>
        </Card>
      ))}
    </Layout>
  );
}

// Templates page
export function Templates() {
  const templates = [
    { id: 'finance', name: 'Finance CV Template', file: '/templates/finance-cv.docx' },
    { id: 'it', name: 'IT CV Template', file: '/templates/it-cv.docx' },
    { id: 'generic', name: 'Generic Cover Letter', file: '/templates/cover-letter.docx' },
  ];
  return (
    <Layout>
      <h1 className="text-xl font-semibold">CV & Cover Letter Templates</h1>
      <ul className="list-disc ml-5">
        {templates.map(t => (
          <li key={t.id}>
            <a href={t.file} download className="text-blue-600">{t.name}</a>
          </li>
        ))}
      </ul>
    </Layout>
  );
}

// Account / Registration page
export function Account() {
  return (
    <Layout>
      <h1 className="text-xl font-semibold">Register for Job Alerts</h1>
      <form className="max-w-md space-y-4">
        <Input placeholder="Full Name" />
        <Input type="email" placeholder="Email Address" />
        <Textarea placeholder="Desired Job Role / Keywords" />
        <Button type="submit">Register</Button>
      </form>
    </Layout>
  );
}

// Main App with routing
export default function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/jobs" element={<Jobs />} />
        <Route path="/interviews" element={<Interviews />} />
        <Route path="/blog" element={<Blog />} />
        <Route path="/templates" element={<Templates />} />
        <Route path="/account" element={<Account />} />
      </Routes>
    </Router>
  );
}
