---
layout: page
permalink: /compositions/
title: compositions
description: Some musical compositions I have written.
nav: true
nav_order: 5
---

<style>
.compositions-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 1.5rem;
  margin-top: 1.5rem;
}

.composition-card {
  background: var(--global-card-bg-color);
  border: 1px solid var(--global-divider-color);
  border-radius: 12px;
  padding: 1.4rem 1.4rem 1.2rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  transition: box-shadow 0.2s ease, transform 0.2s ease;
}

.composition-card:hover {
  box-shadow: 0 4px 18px rgba(0,0,0,0.12);
  transform: translateY(-2px);
}

.composition-card h3 {
  margin: 0;
  font-size: 1.05rem;
  color: var(--global-text-color);
  line-height: 1.3;
}

.composition-links {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.composition-btn {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  padding: 0.45rem 0.8rem;
  border-radius: 8px;
  font-size: 0.875rem;
  font-weight: 500;
  text-decoration: none !important;
  transition: opacity 0.15s ease;
}

.composition-btn:hover { opacity: 0.82; }

.btn-pdf  { background: rgba(220, 53, 69,  0.12); color: #c0392b; }
.btn-midi { background: rgba(13,  110, 253, 0.12); color: #1a6fbf; }
.btn-mp3  { background: rgba(88,  128, 114, 0.18); color: var(--global-theme-color); }

html[data-theme="dark"] .btn-pdf  { background: rgba(220, 53, 69,  0.2); color: #e57373; }
html[data-theme="dark"] .btn-midi { background: rgba(13,  110, 253, 0.2); color: #64b5f6; }
html[data-theme="dark"] .btn-mp3  { background: rgba(88,  128, 114, 0.25); color: var(--global-theme-color); }
</style>

<div class="compositions-grid">

  <div class="composition-card">
    <h3>Flor's Theme</h3>
    <div class="composition-links">
      <a class="composition-btn btn-pdf"  href="/assets/pdf/FlorsThemeScore.pdf"      target="_blank"><i class="fa-solid fa-file-pdf"></i> Sheet Music (PDF)</a>
      <a class="composition-btn btn-midi" href="/assets/audio/FlorsThemeMidi.mid"     download><i class="fa-solid fa-music"></i> MIDI</a>
      <a class="composition-btn btn-mp3"  href="/assets/audio/FlorsThemeMp3.mp3"      download><i class="fa-solid fa-headphones"></i> MP3</a>
    </div>
  </div>

  <div class="composition-card">
    <h3>Cois City</h3>
    <div class="composition-links">
      <a class="composition-btn btn-pdf"  href="/assets/pdf/CoisCityScore.pdf"        target="_blank"><i class="fa-solid fa-file-pdf"></i> Sheet Music (PDF)</a>
      <a class="composition-btn btn-midi" href="/assets/audio/CoisCityMidi.mid"       download><i class="fa-solid fa-music"></i> MIDI</a>
      <a class="composition-btn btn-mp3"  href="/assets/audio/CoisCityMp3.mp3"        download><i class="fa-solid fa-headphones"></i> MP3</a>
    </div>
  </div>

  <div class="composition-card">
    <h3>Pokémon Center Theme — Bossa Nova Remix</h3>
    <div class="composition-links">
      <a class="composition-btn btn-pdf"  href="/assets/pdf/PokemonCenterBossaNovaScore.pdf"  target="_blank"><i class="fa-solid fa-file-pdf"></i> Sheet Music (PDF)</a>
      <a class="composition-btn btn-midi" href="/assets/audio/PokemonCenterBossaNovaMidi.mid" download><i class="fa-solid fa-music"></i> MIDI</a>
      <a class="composition-btn btn-mp3"  href="/assets/audio/PokemonCenterBossaNovaMp3.mp3"  download><i class="fa-solid fa-headphones"></i> MP3</a>
    </div>
  </div>

  <div class="composition-card">
    <h3>Nova City</h3>
    <div class="composition-links">
      <a class="composition-btn btn-pdf"  href="/assets/pdf/NovaCityScore.pdf"        target="_blank"><i class="fa-solid fa-file-pdf"></i> Sheet Music (PDF)</a>
      <a class="composition-btn btn-midi" href="/assets/audio/NovaCityMidi.mid"       download><i class="fa-solid fa-music"></i> MIDI</a>
      <a class="composition-btn btn-mp3"  href="/assets/audio/NovaCityMp3.mp3"        download><i class="fa-solid fa-headphones"></i> MP3</a>
    </div>
  </div>

  <div class="composition-card">
    <h3>Hanera City</h3>
    <div class="composition-links">
      <a class="composition-btn btn-pdf"  href="/assets/pdf/HaneraCityScore.pdf"      target="_blank"><i class="fa-solid fa-file-pdf"></i> Sheet Music (PDF)</a>
      <a class="composition-btn btn-midi" href="/assets/audio/HaneraCityMidi.mid"     download><i class="fa-solid fa-music"></i> MIDI</a>
      <a class="composition-btn btn-mp3"  href="/assets/audio/HaneraCityMp3.mp3"      download><i class="fa-solid fa-headphones"></i> MP3</a>
    </div>
  </div>

</div>

