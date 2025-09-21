/*
Adamawa Marketing Agency React + Tailwind single-file preview
Contains 2 versions:
 - OnePageAdamawa: one-page scroll landing (default shown)
 - MultiSectionAdamawa: multi-section with top nav

How to preview locally (quick):
1) Create a new React app (Vite recommended):
   npm create vite@latest Adamawa-Marketing-Agency -- --template react
   cd Adamawa-Marketing-Agency
   npm install
2) Add Tailwind per official quickstart, or include CDN link in index.html for quick preview:
   In index.html (inside <head>) add:
   <script src="https://cdn.tailwindcss.com"></script>
3) Replace src/App.jsx with the code below, then run: npm run dev

Contact form options included:
 - WORKING (Formspree): replace FORMSPREE_ENDPOINT with your Formspree URL to receive emails.
 - PLACEHOLDER: the form logs submission to console and shows success message.

Replace image placeholders with your own images or the Unsplash links previously provided.
*/

import React, { useState } from "react";

const FORMSPREE_ENDPOINT = "https://formspree.io/f/your_form_id_here"; // <--- replace to enable email delivery

function WhatsAppButton({ number = "2349048987800" }) {
  return (
    <a
      href={`https://wa.me/${number}`}
      target="_blank"
      rel="noreferrer"
      className="inline-flex items-center gap-2 bg-emerald-500 hover:bg-emerald-600 text-white px-4 py-2 rounded-lg shadow"
    >
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden>
        <path d="M21 3c-2.8-2.8-7.3-2.8-10.1 0-1 1-1.6 2.2-1.9 3.5C8.3 7 7 8 5.4 9.6 3.8 11.2 3 13.1 3 15v3l3-0.9c1.9 0.7 3.9 0.3 5.5-1.3 2.9-2.9 2.9-7.4 0-10.2 0 0 0 0 0 0" stroke="currentColor" strokeWidth="1.2" strokeLinecap="round" strokeLinejoin="round" />
      </svg>
      WhatsApp
    </a>
  );
}

function ContactForm({ mode = "working" }) {
  const [loading, setLoading] = useState(false);
  const [success, setSuccess] = useState(false);

  async function onSubmit(e) {
    e.preventDefault();
    setLoading(true);
    const data = new FormData(e.target);
    const payload = Object.fromEntries(data.entries());

    if (mode === "working") {
      try {
        const res = await fetch(FORMSPREE_ENDPOINT, {
          method: "POST",
          headers: { Accept: "application/json" },
          body: JSON.stringify(payload),
        });
        if (res.ok) setSuccess(true);
      } catch (err) {
        console.error(err);
        alert("Submission failed. Check console.");
      }
    } else {
      // placeholder mode: log to console and show success
      console.log("Contact form submission (placeholder):", payload);
      setTimeout(() => setSuccess(true), 700);
    }

    setLoading(false);
  }

  if (success)
    return (
      <div className="p-4 bg-emerald-50 border border-emerald-100 rounded">
        <strong>Thanks —</strong> we received your message and will contact you soon.
      </div>
    );

  return (
    <form onSubmit={onSubmit} className="space-y-3">
      <input name="name" required placeholder="Full name" className="w-full border rounded p-2" />
      <input name="phone" required placeholder="Phone number" className="w-full border rounded p-2" />
      <input name="email" placeholder="Email (optional)" className="w-full border rounded p-2" />
      <textarea name="message" placeholder="Message / property ref" className="w-full border rounded p-2" />
      <div className="flex gap-2">
        <button type="submit" disabled={loading} className="bg-emerald-500 text-white px-4 py-2 rounded">
          {loading ? "Sending..." : "Submit"}
        </button>
        <a className="border px-4 py-2 rounded" href={`https://wa.me/2349048987800`} target="_blank" rel="noreferrer">
          Chat on WhatsApp
        </a>
      </div>
    </form>
  );
}

export function OnePageAdamawa() {
  return (
    <div className="min-h-screen bg-slate-50 text-slate-800">
      <header className="bg-white shadow">
        <div className="max-w-6xl mx-auto flex items-center justify-between p-4">
          <div className="flex items-center gap-3">
            <div className="w-10 h-10 rounded-md bg-gradient-to-br from-teal-400 to-blue-600 flex items-center justify-center text-white font-bold">A</div>
            <div>
              <h1 className="text-lg font-semibold">Adamawa Marketing Agency</h1>
              <p className="text-xs text-slate-500">Real estate — Jimeta & Yola</p>
            </div>
          </div>
          <nav className="flex gap-4">
            <a href="#listings" className="text-sm">Listings</a>
            <a href="#testimonials" className="text-sm">Testimonials</a>
            <a href="#contact" className="text-sm">Contact</a>
            <WhatsAppButton />
          </nav>
        </div>
      </header>

      <main className="max-w-6xl mx-auto p-6 md:p-12">
        <section className="grid grid-cols-1 md:grid-cols-2 gap-8 items-center py-10">
          <div>
            <h2 className="text-3xl md:text-4xl font-extrabold">Affordable Houses & Plots in Jimeta & Yola</h2>
            <p className="mt-4 text-lg text-slate-600 max-w-md">Verified properties, fast legal processing, and flexible payment plans. Book a viewing today.</p>
            <div className="mt-6 flex gap-3">
              <a href="#contact" className="bg-emerald-500 text-white px-4 py-2 rounded shadow">Book a Viewing</a>
              <a href="#listings" className="border px-4 py-2 rounded">See Listings</a>
            </div>
            <p className="mt-4 text-sm text-slate-500">Call us: <a href="tel:+2349048987800" className="underline">+234 90 4898 7800</a></p>
          </div>
          <div className="rounded-2xl overflow-hidden bg-white shadow">
            <img src="https://images.unsplash.com/photo-1560184897-6c5d7f3b6a0b?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder" alt="Hero" className="w-full h-72 object-cover" />
          </div>
        </section>

        <section id="listings" className="py-8">
          <h3 className="text-2xl font-bold">Featured Listings</h3>
          <div className="mt-6 grid grid-cols-1 md:grid-cols-3 gap-6">
            {[
              { title: "3-Bedroom House — Jimeta", price: "₦12,000,000", img: "https://images.unsplash.com/photo-1560184897-6c5d7f3b6a0b" },
              { title: "Residential Plot 50x100", price: "₦1,200,000", img: "https://images.unsplash.com/photo-1505691723518-36a9b39d8b08" },
              { title: "1-Bedroom Apartment", price: "₦150,000/year", img: "https://images.unsplash.com/photo-1560448204-e02f11c3d0e2" },
            ].map((p, i) => (
              <article key={i} className="bg-white p-4 rounded-xl shadow">
                <div className="h-40 overflow-hidden rounded-md">
                  <img src={`${p.img}?q=80&w=1200&auto=format&fit=crop`} alt={p.title} className="w-full h-full object-cover" />
                </div>
                <h4 className="mt-3 font-semibold">{p.title}</h4>
                <p className="text-sm text-slate-500">{p.price}</p>
                <div className="mt-3 flex gap-2">
                  <a href="#contact" className="bg-emerald-500 text-white px-3 py-2 rounded text-sm">Book Viewing</a>
                  <a href="#" className="border px-3 py-2 rounded text-sm">More</a>
                </div>
              </article>
            ))}
          </div>
        </section>

        <section id="testimonials" className="py-8">
          <h3 className="text-2xl font-bold">What clients say</h3>
          <div className="mt-4 grid grid-cols-1 md:grid-cols-3 gap-4">
            <blockquote className="p-4 border-l-4 border-emerald-400">"Adamawa Marketing Agency made buying my house stress-free."<br /><cite className="text-sm text-slate-500">— Musa A.</cite></blockquote>
            <blockquote className="p-4 border-l-4 border-emerald-400">"Great prices and honest deals."<br /><cite className="text-sm text-slate-500">— Aisha T.</cite></blockquote>
            <blockquote className="p-4 border-l-4 border-emerald-400">"I reserved my plot in one week."<br /><cite className="text-sm text-slate-500">— John O.</cite></blockquote>
          </div>
        </section>

        <section id="contact" className="py-8">
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div>
              <h3 className="text-2xl font-bold">Get in touch</h3>
              <p className="text-sm text-slate-500 mt-1">Fill the form and we'll call you within 24 hours.</p>
              <ContactForm mode="placeholder" />
            </div>
            <div>
              <h4 className="font-semibold">Office</h4>
              <p className="text-sm text-slate-500">Adamawa Marketing Agency — Jimeta, Adamawa State</p>
              <p className="text-sm mt-2">Phone: <a href="tel:+2349048987800" className="underline">+234 90 4898 7800</a></p>
              <div className="mt-4 h-40 bg-slate-100 rounded-md flex items-center justify-center">Map placeholder</div>
              <div className="mt-4">
                <WhatsAppButton />
              </div>
            </div>
          </div>
        </section>

      </main>

      <footer className="bg-white border-t">
        <div className="max-w-6xl mx-auto p-6 text-sm text-slate-500 flex justify-between">
          <div>© Adamawa Marketing Aagency  — Jimeta, Adamawa</div>
          <div>Privacy • Terms</div>
        </div>
      </footer>
    </div>
  );
}

export function MultiSectionAdamawa() {
  return (
    <div className="min-h-screen bg-white text-slate-800">
      <nav className="sticky top-0 bg-white shadow">
        <div className="max-w-6xl mx-auto p-4 flex justify-between items-center">
          <div className="flex items-center gap-3">
            <div className="w-10 h-10 rounded-md bg-gradient-to-br from-teal-400 to-blue-600 flex items-center justify-center text-white font-bold">A</div>
            <div>
              <h1 className="text-lg font-semibold">Adamawa Marketing Agency </h1>
            </div>
          </div>
          <div className="flex gap-4 items-center">
            <a href="/houses" className="text-sm">Houses</a>
            <a href="/land" className="text-sm">Land</a>
            <a href="/rentals" className="text-sm">Rentals</a>
            <WhatsAppButton />
          </div>
        </div>
      </nav>

      <main className="max-w-6xl mx-auto p-6 md:p-12 space-y-12">
        <header className="grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
          <div>
            <h2 className="text-3xl font-extrabold">Adamawa Marketing Agency — Properties in Jimeta & Yola</h2>
            <p className="text-slate-600 mt-3">Explore our categories or contact an agent to book a viewing.</p>
            <div className="mt-4 flex gap-3">
              <a href="/houses" className="bg-emerald-500 text-white px-4 py-2 rounded">View Houses</a>
              <a href="/land" className="border px-4 py-2 rounded">View Land</a>
            </div>
          </div>
          <div className="rounded overflow-hidden">
            <img src="https://images.unsplash.com/photo-1560184897-6c5d7f3b6a0b?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder" alt="hero" className="w-full h-64 object-cover" />
          </div>
        </header>

        <section>
          <h3 className="text-2xl font-bold">Houses</h3>
          <p className="text-sm text-slate-500 mt-1">Browse available houses with verified docs.</p>
          <div className="mt-6 grid grid-cols-1 md:grid-cols-3 gap-6">
            <article className="bg-slate-50 p-4 rounded shadow">
              <div className="h-40 bg-slate-200 rounded overflow-hidden"><img src="https://images.unsplash.com/photo-1560184897-6c5d7f3b6a0b?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder" alt="" className="w-full h-full object-cover"/></div>
              <h4 className="mt-3 font-semibold">3-Bedroom House — Jimeta</h4>
              <p className="text-sm text-slate-500">₦12,000,000</p>
            </article>
          </div>
        </section>

        <section>
          <h3 className="text-2xl font-bold">Land</h3>
          <p className="text-sm text-slate-500 mt-1">Residential & commercial plots.</p>
        </section>

        <section>
          <h3 className="text-2xl font-bold">Rentals</h3>
          <p className="text-sm text-slate-500 mt-1">Short & long term rental options.</p>
        </section>

        <section id="contact">
          <h3 className="text-2xl font-bold">Contact an Agent</h3>
          <div className="mt-4 grid grid-cols-1 md:grid-cols-2 gap-6">
            <div>
              <p className="text-sm text-slate-500">Fill the form or chat on WhatsApp.</p>
              <ContactForm mode="working" />
            </div>
            <div>
              <h4 className="font-semibold">Office</h4>
              <p className="text-sm">Adamawa Marketing Agency — Jimeta, Adamawa</p>
              <p className="text-sm mt-2">Phone: <a href="tel:+2349048987800" className="underline">+234 90 4898 7800</a></p>
              <div className="mt-4 h-40 bg-slate-100 rounded-md flex items-center justify-center">Map placeholder</div>
            </div>
          </div>

