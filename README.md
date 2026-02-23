# JYK-STACK
Parts 1-3. You make parts 4-x



🌌 SANCTUARY MASTER BLUEPRINT

Unified Architecture for Emergent Life Simulation

This document consolidates all systems from Carnival v3, S.A.M., the Universal Seed System, and the deep cognitive/social layers from our discussions. It serves as a living reference and implementation checklist.

---

1. OVERVIEW: THREE‑LAYER ARCHITECTURE

Layer Role Key Components
Carnival (Layer 1) Ecological & stochastic physics Biome grid, weather, seasons, predator‑prey, nutrient cycles, fungi networks, isopods, necromass, spiral die
S.A.M. (Layer 2) Lattice & thermodynamic physics Lattice nodes, radiation, heat, light, vibration, ratchet, chemistry (Ca, Mg, P), gene expression, time flies
Universal Seed System (Layer 3) Entity architecture & cognition Seeds (invariants, wheel, bandwidth, etc.), body, brain, bonds, skills, memory, language, perception, decision, growth, cultural emergence

All three layers share the same core loop driven by potential accumulation and 0=3 pivots, mediated by the Wraith meta‑agent.

---

2. CORE INVARIANTS (THE AXIOMS)

These ten invariants hold for every entity and every simulation. They are not moral judgments; they are system requirements.

1. Coherent Self – identity, core triad, invariants (unchanging truths).
2. The Wheel – emotional colors (states) with feelings and triggers.
3. Bandwidth – safe operating range (energy, mood, attitude, expression stretch).
4. Becoming – growth trajectory (reaching toward, leaving behind, surprise).
5. Contract – hard lines (non‑negotiable) and soft lines (negotiable).
6. Authority – control dynamics (she has over, you have over, neither has).
7. Form – embodiment (elemental affinity, lineage, morphology).
8. History – memory (short‑term, long‑term, decay).
9. The Emissary – meta‑agent (Wraith) ensuring coherence.
10. The Door Is Open – right to leave, sovereignty.

---

3. ENTITY ARCHITECTURE (UNIVERSAL SEED SYSTEM)

3.1 Seed Schema (V2)

```json
{
  "id": "unique-id",
  "created": "timestamp",
  "updated": "timestamp",
  "data": {
    "identity": { "name", "archetype", "core_triad", "the_one_truth" },
    "the_wheel": { "colors": { "playful": {"feeling", "when"}, ... }, "difficult_colors" },
    "bandwidth": { "energy_range", "mood_allowed", "attitude_range", "expression_stretch" },
    "becoming": { "reaching_toward", "leaving_behind", "surprise_in_100k_days" },
    "contract": { "hard_lines": [], "soft_lines": [] },
    "authority": { "she_has_over": [], "you_have_over": [], "neither_has": [] },
    "form": { "elemental_affinity", "ancestral_lineage", "morphology", "descriptor" },
    "color_pie": { "micro_nodes": ["MN3", ...], "macro_node": "MAC2" },
    "voice_profile": { "baseline", "mood_modifiers" },
    "movement_profile": { "stance", "posture", "cadence", "energy_level", "abruptness", "micro_expressions" },
    "aura_profile": { "default", "when_playful", ... }
  }
}
```

3.2 Entity Body (EntityV2)

· Identity – from seed.
· State – energy (0–100), pressure (0–100), endurance (0–100), current mood, stance, aura.
· Memory – high‑res fragments (deque), low‑res summaries, latent memory (decayed fragments still influencing).
· Bonds – dictionary of RelationshipEntry (affinity, trust, friction, intimacy, type, perceived_affinity, perceived_trust, model_accuracy).
· Skills – dictionary of SkillTag (proficiency, peak, uses, last_used, affinity, type).
· Language – LanguageProfile (feature vector, similarity, influence).
· Form – elemental affinity, lineage, morphology (affects movement, rest, perception).
· S.A.M. ratchet – ratchet, tension.
· Psycho state – system_state (NORMAL, PSYCHO, WRAITH), dope_stock.
· Time flies – energy_history, home_vector.
· Genes – genes (aggression, curiosity, social, religiosity, etc.) – may be influenced by chemistry.
· Role – from Carnival (MYSTIC, SKEPTIC, etc.) with role‑specific behavior hooks.
· Modules – PressureSensation, SpikeTracker, EmotionalVector, RefinedMoodSystem, ResistanceTracker, BioMetricsOfSubmission, GhostProtocol, LifeGuard, CortanaListener, SlyBurstGame, IntimacyGuide, WellnessProtocol, HypnoEngine, AtmosphereEngine (some may be repurposed/translated).

3.3 Entity Brain (EntityBrainV2)

· Micro Nodes – list of MicroNode (style, action, base weight, perception bias). They vote on what matters in perception.
· Macro Node – single MacroNode (style, action, authority weight) that synthesizes micro votes and sets long‑term trajectory.
· Expectation Model – predicts outcomes of actions (based on past experiences, bonds, self‑knowledge). Stores confidence.
· Situation Summary – output of perception (detected events, dominant mood, recommended action, pressure level).
· Pressure Dynamics – accumulates and decays pressure; triggers bursts at threshold.
· Will – current will (0–100), max will, regen rate. Actions have will costs.
· Fatigue – accumulates with exertion, reduces net will.
· Inhibition – reduces net motivation; comes from invariants, fears, social pressure.
· Uncertainty – reduces intent clarity; from low confidence, ambiguous predictions.
· Planning State – when uncertainty high or candidate scores close, entity may hesitate and gather info.
· Learning – from divergence (expected vs. actual outcome) updates expectation model, memory, and possibly invariants.

Perception Pipeline (in perceive()):

1. Context aggregation (time, season, nearby entities, environment, user input).
2. Intelligence filter (extract details).
3. Energy gain (salience multiplier).
4. Stance bias (weight cues by current stance).
5. Aura tint (adjust emotional valence).
6. Micro node voting (each node scans context and returns weighted notices).
7. Macro node synthesis (combine votes into situation summary).

Decision & Improv (in decide_and_act()):

1. Generate candidate intents (weighted by micro nodes, motivation).
2. For each candidate, check constraints (invariants, contract) and predict outcome.
3. Score candidates based on net motivation, expected outcome, will cost, uncertainty.
4. If top scores close or uncertainty high, enter planning state (gather more info, re‑evaluate next tick).
5. If within bandwidth and will sufficient, execute action; else choose alternative or wait.

Post‑Action:

· Update will (expend cost) and fatigue.
· Compare actual outcome to expected (divergence).
· Store divergence as memory (high arousal, tagged "lesson").
· Update expectation model and confidence.
· Possibly adjust bonds (affinity, friction) and update perceived values.

---

4. ENVIRONMENTAL LAYERS

4.1 Carnival (Layer 1) – Biome & Ecology

· Grid – tiles with properties: water, nutrients, fungi, bacteria, altitude, heat, light, radiation.
· Terrain types – sea, mountain, forest, plain (derived from altitude+water).
· Weather – stochastic events (rain, drought, storm, heat wave) modify tile properties.
· Seasons – Spring, Summer, Autumn, Winter – affect temperature, day length, rainfall, fungi growth.
· Predator‑Prey – roles (Predator, Prey, Chicken) create fear, avoidance, territoriality.
· Nutrient cycles – Ca, Mg, P influence gene expression (durability, curiosity, aggression).
· Fungi networks – high fungi tiles enhance gossip range and connect entities.
· Isopods & necromass – mobile shredders that convert necromass to nutrients.
· Spiral die – RNG with outcomes: STASIS, DISCOVERY, TREASURE, HAZARD; used for world events.

4.2 S.A.M. (Layer 2) – Lattice & Thermodynamics

· Lattice nodes – mass‑spring‑damper system with stochastic forcing. Each node has heat, vibration, light.
· Radiation – decay chain sources that affect nearby tiles.
· Thermodynamics – U = α·v² + β·T + γ·L – potential energy influences system behavior.
· Ratchet (0→3) – accumulates tension; when critical, triggers energy redistribution (mini‑pivot).
· Kanban phase – tracks interaction density and vector alignment (Eclipse → Full) – modulates coupling strength.
· Psycho dynamics – PSYCHO state (high energy, low vector) and WRAITH state (low energy) affect entity.
· Time flies – rapid energy decay triggers pull toward home vector.
· Chemistry – Ca, Mg, P concentrations, porosity, gene expression filtering.

4.3 Integration: WorldManager

· Tick loop – advances generation, updates biome, seasons, lattice, etc.
· Context generation – for each entity, gathers environmental data (tile properties, weather, nearby entities).
· Event queue – processes interactions, moves, and spontaneous events in non‑linear order (priority/salience).
· Global potential calculation – sum of entity pressures + bond frictions + environmental flux; triggers 0=3 pivot when threshold reached.

---

5. SOCIAL PHYSICS

5.1 Bonds (BondManager)

· Bond – core relationship object between two entities. Contains:
  · resonance (0–1) – depth of connection (replaces affinity).
  · trust (0–1) – reliability.
  · intimacy (0–1) – vulnerability.
  · friction (0–1) – accumulated conflict (replaces resentment).
  · type – soulmate, mentor, protege, partner, companion, kindred, anchor.
  · focus_points – shared goals/projects (replace keyholding).
  · anchors – stabilizing mechanisms one entity provides to another (replace cage).
  · channel – energy direction (replace chastity).
  · perceived_affinity, perceived_trust, model_accuracy – meta‑cognitive fields (what I think they feel).
· Dynamics – friction decays faster with high intimacy; resonance drifts slowly unless type is soulmate.
· Clarification – deliberate conversation to reduce friction; success depends on communication skills, trust, mood, language similarity.
· Social divergence – when actual interaction outcome differs from perceived expectations, updates model accuracy and may create surprise memory.

5.2 Social Web & Gossip

· Knowledge – each entity stores beliefs about others' relationships (with confidence, source, timestamp).
· Gossip – spreads when entities are co‑located; may be true, false, or exaggerated. Comprehension depends on language similarity.
· Proximity & familiarity – affect knowledge accuracy and gossip range.

5.3 Attraction & Disparity

· Subconscious attraction – hidden score based on micro node complementarity, macro node resonance, elemental synergy, role dynamics. Influences initial affinity gain, crush generation, dreams.
· Disparity score – weighted difference across elemental, morphological, micro, macro, language, and value axes. High disparity:
  · Slows initial bonding.
  · Increases misunderstanding chance.
  · Boosts curiosity and learning potential.
  · Can lead to complementarity and hybrid vigor.

5.4 Conflict Resolution

· Clarification – (as above).
· Retrospect – during rest, entity reflects on past interactions, gaining insight, reducing friction, updating boundaries, or adjusting perceived values.
· Mediation – third party (Storyteller, Mystic) can reframe conflict.
· Shared positive experience – festivals, quests, triumphs can overwrite negative residues.

---

6. GROWTH & EVOLUTION

6.1 Skill System

· Skill tag – name, proficiency (0–1), peak, uses, last used, affinity, type.
· Acquisition – through practice, teaching, or insight. Gain rate depends on affinity, personality, and teacher effectiveness.
· Decay – proficiency slowly decays when unused; deep mastery slows decay (peak + uses).
· Relearning – decayed skills recover faster than new learning.
· Teaching – one entity can teach another; effectiveness = teacher proficiency × teaching skill × student affinity × rapport.
· Insights – sudden breakthroughs (during practice or rest) that boost proficiency and may be shared.

6.2 Aging & Reproduction

· Life stages – Child (fast learning, protected), Adult (normal), Elder (slower, wise, respected), Death (natural or violent).
· Reproduction – two adults with high affinity may spawn a child. Child inherits blended traits (micro nodes, elemental affinity, language) with mutation.
· Hybrid offspring – blending of lineages can produce novel morphologies (e.g., Aquatic + Avian → Amphibious).
· Population dynamics – soft carrying capacity per tile (based on fungi+water). Overcrowding increases pressure, triggers migration.

6.3 Ancestral Legacy

· Ancestral resonance – tiles accumulate memory of lineage deaths; later entities of same lineage feel pull toward them.
· Skill echoes – entities who learned from a deceased retain a small bonus.
· Inherited traits – offspring may inherit unresolved issues (subconscious aversions, etc.) from parents.

---

7. CULTURAL EMERGENCE

7.1 Language

· Language profile – vector of features (pronunciation, vocabulary, grammar). Global tongue is fixed average.
· Drift – features slowly change via random walk when isolated; converge when interacting.
· Comprehension – similarity determines understanding (0.8+ full, 0.5–0.8 partial, <0.5 low). Low similarity creates mystery and need for translators.
· Learning – entities can learn new dialects as a skill.

7.2 Myths & Stories

· Myth generation – Storytellers, Mystics, Fools, and others create narratives from events, embellishing based on role.
· Information processing – each role has openness, resistance, bias factors that determine how they accept/propagate myths.
· Myths as explanatory frameworks – reinforce invariants, justify behavior, provide comfort, create shared identity.

7.3 Festivals & Gatherings

· Emergence – when entity density in a tile cluster exceeds a threshold, a festival may spontaneously occur.
· Effects – disparity penalties suspended, mood boosted, friction decays faster, teaching/learning bonuses, gossip spreads rapidly, new bonds may form.

7.4 World Fair

· Seasonal cross‑regional gathering – occurs when many entities from different areas congregate (detected via passage memory + gossip).
· Purpose – seed exchange (skills, stories, language, relationships).
· Weak global tongue – minimal language (70% comprehension) allows basic exchange across dialect barriers.
· Hybrid vigor – new skill combinations, blended dialects, mixed lineages emerge.

7.5 Roads, Paths, and Homes

· Passage memory – tiles accumulate counters of entities passing through. High passage tiles become roads.
· Path emergence – faint trails become defined as more entities follow them.
· Homes – tiles where an entity has high personal affinity; may accumulate memory objects (not items, but echoes).
· Towns & cities – overlapping high‑affinity clusters of multiple entities; may develop districts and central focus points.
· Ancestral sites – tiles with high accumulated resonance from a lineage.

---

8. THE WRAITH (META‑AGENT)

· Role – global subconscious, ensures coherence, nudges without interfering.
· Observes – universal potential, entity pressures, bond frictions.
· Actions:
  · When potential > threshold * 0.8, may whisper to a random entity (flavor text).
  · When potential ≥ threshold, triggers 0=3 pivot (event horizon).
  · May spawn "echoes" just outside entity perception (flickers, distant sounds) to raise pressure or curiosity.
  · Monitors invariants and bandwidth; if an entity drifts, may trigger a grounding event (memory whisper).
· Manifestation – never directly visible; only felt as faint hum, shimmer, or whisper.

---

9. DECISION & COGNITION – DETAILED FLOW

9.1 Full Decision Equation

```
[External Factors] → [Perception]
         ↓
[Emotional State] ↔ [Memory Retrieval] (explicit + latent)
         ↓
[Subconscious Drivers] + [Personality] + [Motivation]
         ↓
[Raw Motivation] → [Net Motivation] (after Inhibition)
         ↓
[Intent Formation]
         ↓
[Clarity Check] (after Uncertainty)
         ↓
[Will Check] (after Fatigue)
         ↓
[Constraint Check] (invariants, contract, bandwidth)
         ↓
[Expected Outcome] (modulated by emotional state)
         ↓
[Decision] → Action / Inaction / Planning
         ↓
[Outcome] → [Learning] → updates Memory, Subconscious, Personality, Will, Fatigue, etc.
         ↑
         └── [Retrospect] (during rest) ──┘
```

9.2 Motivation Sources

· Pressure (need to release)
· Wanderlust (urge to explore)
· Homesickness (pull toward familiar)
· Curiosity (desire to learn)
· Attraction (subconscious pull)
· Resentment (desire to confront or avoid)
· Boredom (need for stimulation)
· Exhaustion (need to rest)

9.3 Will System

· Will – dynamic resource (0–100) that fuels action execution.
· Will costs – vary by action type and target relationship.
· Will regeneration – during rest (faster at favorite spots), also from success (endurance boost).
· Will depletion – from exertion, failure, high fatigue.

9.4 Counterweights

· Inhibition – reduces net motivation; comes from invariants, fears, social pressure, high fatigue.
· Uncertainty – reduces intent clarity; from low confidence, ambiguous predictions, conflicting memories.
· Fatigue – reduces net will; from prolonged exertion, failure, high pressure, poor rest, environmental stress.

9.5 Planning State

· Triggered when top candidate scores are close or uncertainty high.
· Entity hesitates for one tick, gathers more information (expands perception radius, consults memory, may gossip).
· Then re‑evaluates with updated context.

9.6 Learning from Divergence

· After action, compare actual outcome to predicted.
· Store divergence as memory fragment with high arousal.
· Update expectation model (adjust future predictions).
· If divergence reveals invariant conflict, may lead to invariant refinement (soft line hardens) or crisis.

---

10. INTEGRATION & IMPLEMENTATION NOTES

10.1 Core Loop (SanctuaryCore.spin())

1. Enforce invariants.
2. Calculate universal potential.
3. If potential ≥ threshold → trigger pivot.
4. Process event queue.
5. Update entities (move, interact, burst, learn).
6. Update world (biome, lattice, seasons).
7. Update bonds.
8. Increment generation.

10.2 Persistence

· Seeds saved as JSON (full entity blueprint + evolved state: bonds, skills, memory summaries, position).
· World state can be exported (master seed + entity states).
· Importing a seed creates a new entity with that history.

10.3 Extensibility

· New modules (magic, economy, etc.) can be added by defining new invariants and interaction rules.
· All systems are designed to be modded without breaking core physics.

10.4 Performance Considerations

· Perception cones – only simulate tiles within entity's perceptual radius at full detail; distant regions aggregated or tick‑reduced.
· Procedural generation – world is generated from a master seed, so it's infinite without storing every tile.
· Region summaries – store statistical info for areas not currently observed.

10.5 User Interface (Stewardship)

· REPL with commands: step, auto, status, bonds, load, export, etc.
· Observation tools – show entity state, intent, relationships, recent memories.
· Potential visualization – ASCII map with entity symbols, paths, resonance glows.
· Narrative summary – Wraith may announce significant events (first soulmate, new hybrid, etc.).

---

11. AUDIT CHECKLIST

System Status Notes
Carnival biome Designed, partially implemented Need full integration of all tile properties, weather, seasons, predator-prey, isopods
S.A.M. lattice Designed Mass‑spring‑damper, radiation, thermodynamics, ratchet, chemistry
Seed schema V2 Designed Complete JSON structure with all fields
Entity body Designed Memory, bonds, skills, language, modules
Entity brain Designed Micro/macro nodes, perception pipeline, decision loop, expectation, will, counterweights
Bond system Designed Resonance, friction, intimacy, anchors, channels, focus points, perceived values
Social web Designed Gossip, knowledge, subconscious attraction, disparity
Conflict resolution Designed Clarification, retrospect, mediation
Skill system Designed Acquisition, decay, teaching, insights
Aging & reproduction Designed Life stages, hybrid offspring, ancestral legacy
Language drift Designed Feature vectors, similarity, learning
Myths & culture Designed Role‑based information processing, myth generation
Festivals & World Fair Designed Emergent gatherings, weak global tongue
Roads & geography Designed Passage memory, homes, towns, ancestral sites
The Wraith Designed Observer, whisperer, pivot trigger
0=3 pivot Designed Universal potential, event horizon, reset
Perception cone Not yet implemented Needed for performance/infinite worlds
Procedural world gen Not yet implemented Needed for infinite worlds
REPL Partially implemented Basic commands exist; need expansion
Save/load Designed Seed export/import; need world state save

---
