<script setup>
import { getRuleById } from '~/data/rules'

const ruleId = 178
const rule = getRuleById(ruleId)
const activeTab = ref('preview')
</script>

<template>
  <section v-if="rule" class="space-y-6">
    <!-- Header -->
    <header class="space-y-3">
      <button
        @click="$router.back()"
        class="inline-flex items-center gap-2 text-sm text-zinc-400 hover:text-zinc-200 transition"
      >
        ← Retour
      </button>
      <div class="text-sm text-zinc-400">Règle n° {{ rule.id }}</div>

      <h1
        class="text-2xl sm:text-3xl font-semibold tracking-tight text-zinc-100"
      >
        {{ rule.title }}
      </h1>

      <div class="text-base sm:text-sm tracking-tight text-zinc-300">
        {{ rule.description }}
      </div>

      <div class="flex flex-wrap gap-2">
        <span
          v-for="tag in rule.tags"
          :key="tag"
          class="text-xs rounded-full border border-zinc-800 bg-zinc-900/30 px-2.5 py-1 text-zinc-300"
        >
          {{ tag }}
        </span>
      </div>

      <div
        v-if="rule.authors && rule.authors.length"
        class="text-sm text-zinc-400"
      >
        Écrit par
        <span class="text-zinc-300">
          {{ rule.authors.join(', ') }}
        </span>
      </div>
    </header>

    <!-- Objectif -->
    <section class="rounded-2xl border border-zinc-800 bg-zinc-900/30 p-6">
      <h2 class="text-lg font-semibold tracking-tight text-zinc-100">
        Objectif
      </h2>

      <ul class="mt-1 list-disc pl-5 space-y-2 text-sm text-zinc-300">
        <li v-for="o in rule.objectives" :key="o">{{ o }}</li>
      </ul>
    </section>

    <!-- Mise en œuvre -->
    <section class="rounded-2xl border border-zinc-800 bg-zinc-900/30 p-6">
      <h2 class="text-lg font-semibold tracking-tight text-zinc-100">
        Mise en œuvre
      </h2>

      <p v-if="rule.implementationIntro" class="mt-3 text-sm text-zinc-400">
        {{ rule.implementationIntro }}
      </p>

      <ul class="mt-1 list-disc pl-5 space-y-2 text-sm text-zinc-300">
        <li v-for="x in rule.implementation" :key="x">{{ x }}</li>
      </ul>
    </section>

    <!-- Contrôle -->
    <section class="rounded-2xl border border-zinc-800 bg-zinc-900/30 p-6">
      <h2 class="text-lg font-semibold tracking-tight text-zinc-100">
        Contrôle
      </h2>

      <ul class="mt-3 list-disc pl-5 space-y-2 text-sm text-zinc-300">
        <li v-for="c in rule.control" :key="c">{{ c }}</li>
      </ul>
    </section>

    <!-- Exemples -->
    <section class="space-y-4">
      <h2 class="text-lg font-semibold tracking-tight text-zinc-100">
        Exemples
      </h2>

      <div
        class="rounded-2xl border border-zinc-800 bg-zinc-900/30 overflow-hidden"
      >
        <!-- Tabs -->
        <div class="flex border-b border-zinc-800">
          <button
            @click="activeTab = 'preview'"
            :class="[
              'px-5 py-3 text-sm transition',
              activeTab === 'preview'
                ? 'text-zinc-100 border-b-2 border-zinc-100'
                : 'text-zinc-400 hover:text-zinc-200',
            ]"
          >
            Rendu
          </button>

          <button
            @click="activeTab = 'code'"
            :class="[
              'px-5 py-3 text-sm transition',
              activeTab === 'code'
                ? 'text-zinc-100 border-b-2 border-zinc-100'
                : 'text-zinc-400 hover:text-zinc-200',
            ]"
          >
            Code
          </button>
        </div>

        <!-- Content -->
        <div class="p-6">
          <!-- RENDU -->
          <div v-if="activeTab === 'preview'" class="space-y-4">
            <div class="text-sm text-zinc-400">
              Liste des newsletters accessible depuis le site.
            </div>

            <div class="rounded-xl border border-zinc-800 bg-zinc-950 p-6">
               <h3 class="text-zinc-100 font-semibold mb-4">Archives Newsletters</h3>
               <div class="space-y-2">
                  <a href="#" class="block p-3 rounded-lg border border-zinc-800 hover:bg-zinc-900 transition flex justify-between items-center group">
                     <div>
                        <div class="text-sm font-medium text-zinc-200 group-hover:text-blue-400 transition">Janvier 2026 : Les nouveautés de l'année</div>
                        <div class="text-xs text-zinc-500">Envoyée le 05/01/2026</div>
                     </div>
                     <span class="text-zinc-500 text-xs">Lire online &rarr;</span>
                  </a>
                  <a href="#" class="block p-3 rounded-lg border border-zinc-800 hover:bg-zinc-900 transition flex justify-between items-center group">
                     <div>
                        <div class="text-sm font-medium text-zinc-200 group-hover:text-blue-400 transition">Décembre 2025 : Rétrospective</div>
                        <div class="text-xs text-zinc-500">Envoyée le 15/12/2025</div>
                     </div>
                     <span class="text-zinc-500 text-xs">Lire online &rarr;</span>
                  </a>
               </div>
            </div>
          </div>

          <!-- CODE -->
          <div v-else>
            <pre
              class="rounded-xl bg-zinc-950 p-5 overflow-x-auto text-sm text-zinc-100"
            >
<code>
&lt;ul class=&quot;archive-list&quot;&gt;
  &lt;li&gt;
    &lt;a href=&quot;/newsletters/2026-01&quot;&gt;
      &lt;strong&gt;Janvier 2026&lt;/strong&gt; : Les nouveautés de l'année
    &lt;/a&gt;
    &lt;span class=&quot;date&quot;&gt;(Envoyée le 05/01/2026)&lt;/span&gt;
  &lt;/li&gt;
  &lt;li&gt;
    &lt;a href=&quot;/newsletters/2025-12&quot;&gt;
      &lt;strong&gt;Décembre 2025&lt;/strong&gt; : Rétrospective
    &lt;/a&gt;
    &lt;span class=&quot;date&quot;&gt;(Envoyée le 15/12/2025)&lt;/span&gt;
  &lt;/li&gt;
&lt;/ul&gt;
</code>
</pre>

            <p class="mt-3 text-xs text-zinc-500">
              Les archives permettent aux nouveaux inscrits de voir le contenu passé et améliorent le référencement naturel.
            </p>
          </div>
        </div>
      </div>
    </section>
  </section>

  <section v-else class="rounded-2xl border border-zinc-800 bg-zinc-900/30 p-6">
    <h1 class="text-lg font-semibold text-zinc-100">Règle introuvable</h1>
    <p class="mt-2 text-sm text-zinc-400">
      Vérifiez que la règle existe dans
      <code class="text-zinc-300">rules.json</code>.
    </p>
  </section>
</template>
