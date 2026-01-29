<script setup>
import { getRuleById } from '~/data/rules'

const ruleId = 176
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
              Interface de gestion des abonnements accessible depuis le compte utilisateur.
            </div>

            <div class="rounded-xl border border-zinc-800 bg-zinc-950 p-6 max-w-md mx-auto">
              <h3 class="text-base font-semibold text-zinc-100 mb-4 border-b border-zinc-800 pb-2">
                Mes préférences emails
              </h3>
              
              <div class="space-y-4">
                <label class="flex items-start gap-3 p-3 rounded-lg bg-zinc-900/50 hover:bg-zinc-900 transition cursor-pointer">
                  <input type="checkbox" checked class="mt-1 rounded border-zinc-700 bg-zinc-800 text-green-600 focus:ring-green-600/20" />
                  <div>
                    <div class="text-sm font-medium text-zinc-200">Newsletter Hebdo</div>
                    <div class="text-xs text-zinc-500">Les meilleures actus de la semaine, chaque lundi.</div>
                  </div>
                </label>

                <label class="flex items-start gap-3 p-3 rounded-lg bg-zinc-900/50 hover:bg-zinc-900 transition cursor-pointer">
                  <input type="checkbox" class="mt-1 rounded border-zinc-700 bg-zinc-800 text-green-600 focus:ring-green-600/20" />
                  <div>
                    <div class="text-sm font-medium text-zinc-200">Offres partenaires</div>
                    <div class="text-xs text-zinc-500">Promotions exclusives de nos partenaires.</div>
                  </div>
                </label>
              </div>

              <div class="mt-6 flex justify-end">
                <button class="px-3 py-1.5 bg-zinc-100 text-zinc-900 text-xs font-semibold rounded hover:bg-zinc-200 transition">
                  Enregistrer mes choix
                </button>
              </div>
            </div>
          </div>

          <!-- CODE -->
          <div v-else>
            <pre
              class="rounded-xl bg-zinc-950 p-5 overflow-x-auto text-sm text-zinc-100"
            >
<code>
&lt;form class=&quot;p-6 bg-zinc-950 rounded-xl&quot;&gt;
  &lt;h3&gt;Mes préférences emails&lt;/h3&gt;
  
  &lt;label class=&quot;flex gap-3 p-3&quot;&gt;
    &lt;input type=&quot;checkbox&quot; name=&quot;newsletter_weekly&quot; checked /&gt;
    &lt;div&gt;
      &lt;div&gt;Newsletter Hebdo&lt;/div&gt;
      &lt;small&gt;Les meilleures actus de la semaine.&lt;/small&gt;
    &lt;/div&gt;
  &lt;/label&gt;

  &lt;label class=&quot;flex gap-3 p-3&quot;&gt;
    &lt;input type=&quot;checkbox&quot; name=&quot;partners&quot; /&gt;
    &lt;div&gt;
      &lt;div&gt;Offres partenaires&lt;/div&gt;
      &lt;small&gt;Promotions exclusives.&lt;/small&gt;
    &lt;/div&gt;
  &lt;/label&gt;

  &lt;button type=&quot;submit&quot;&gt;Enregistrer&lt;/button&gt;
&lt;/form&gt;
</code>
</pre>

            <p class="mt-3 text-xs text-zinc-500">
              L'utilisateur peut modifier ses choix à tout moment depuis son espace personnel, sans avoir besoin de retrouver un e-mail reçu.
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
