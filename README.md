"use client";

import { useState } from "react";

export default function PMaxPreviewStudio() {
  const [headline, setHeadline] = useState(
    "Book Flights to New Zealand"
  );

  const [longHeadline, setLongHeadline] = useState(
    "Discover amazing fares to New Zealand with Air New Zealand"
  );

  const [description, setDescription] = useState(
    "Explore Auckland, Queenstown and Christchurch with flexible booking options."
  );

  const [businessName, setBusinessName] =
    useState("Air New Zealand");

  const [url, setUrl] = useState(
    "www.airnewzealand.com.au"
  );

  const [cta, setCta] =
    useState("Book Now");

  const countColor = (count, limit) => {
    if (count > limit) return "text-red-500";
    if (count > limit * 0.9) return "text-orange-500";
    return "text-green-600";
  };

  return (
    <div className="min-h-screen bg-slate-100 p-8">
      <div className="max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-2 gap-8">
        
        {/* LEFT SIDE */}
        <div className="bg-white rounded-xl shadow p-6">
          <h1 className="text-2xl font-bold mb-6">
            PMax Preview Studio
          </h1>

          <div className="space-y-5">

            <div>
              <label className="font-semibold block mb-2">
                Business Name
              </label>
              <input
                value={businessName}
                onChange={(e) =>
                  setBusinessName(e.target.value)
                }
                className="w-full border rounded-lg p-3"
              />
            </div>

            <div>
              <label className="font-semibold block mb-2">
                Final URL
              </label>
              <input
                value={url}
                onChange={(e) =>
                  setUrl(e.target.value)
                }
                className="w-full border rounded-lg p-3"
              />
            </div>

            <div>
              <label className="font-semibold block mb-2">
                Headline
              </label>

              <
