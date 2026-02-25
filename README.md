## Test Files → REQUIREMENTS Mapping

### Particle Physics (Requirement 1)

| Test File | Requirement Tested |
|:---|:---|
| `test_air_straight_line.JSON` | Air moves in a straight line, bouncing off solids (3 particles, varied velocities) |
| `test_dust_gravity_random.JSON` | Dust has slight gravity and randomly moves left/right each frame (3 particles, open space) |
| `test_fire_spawns_lightning.JSON` | Fire is stationary and shoots lightning sparks in different directions over time |
| `test_water_gravity.JSON` | Water drips down (3 particles in open space) |
| `test_water_slide.JSON` | Water slides sideways to find the lowest level when hitting something solid |
| `test_water_fire_interaction.JSON` | Water touching fire turns into upward-moving air |
| `test_water_fire_chain.JSON` | Full chain: multiple water drops falling toward fire at bottom |
| `test_earth_stationary.JSON` | Earth is always stationary and solid (row of earth blocks) |
| `test_lightning_straight_line.JSON` | Lightning travels in a straight line and stops when hitting something solid |
| `test_lightning_water_interaction.JSON` | Lightning touching water turns the water into lightning |
| `test_lightning_earth_to_dirt.JSON` | Lightning hitting earth turns it into dirt |
| `test_dirt_pile.JSON` | Dirt travels downward and forms piles on solid surfaces |
| `test_water_pool_basin.JSON` | Water settling into a U-shaped earth basin — full water flow behavior |
| `test_fire_earth_chain.JSON` | Full chain: fire → lightning → lightning hits earth → earth becomes dirt |

---

### World Class (Requirement 2)

| Test File | Requirement Tested |
|:---|:---|
| `test_boundary_deletion.JSON` | Particles leaving the boundary are deleted (4 air particles toward each edge) |
| `test_size_alive_count.JSON` | `World::size()` and `World::alive_count()` — 5 particles with varying lifetimes |
| `test_save_load_roundtrip.JSON` | `World::save()` and `World::load()` — complex multi-type scene round-trip |
| `test_empty_world.JSON` | Edge case: empty world — tests `physics()`, `size()`, `alive_count()` |
| `test_duplicate_position.JSON` | No two particles can occupy the same location (two particles at `(10,10)`) |

---

### Lifetime & Stationary (Requirement 1 Subsections)

| Test File | Requirement Tested |
|:---|:---|
| `test_lifetime_decrement.JSON` | Lifetime decrements by 1 per frame; deleted at exactly 0. Particles with lifetimes 1, 3, 5 + one earth with `-1` |
| `test_stationary_behavior.JSON` | Stationary particles are solid and don't move, but can still be transformed (stationary water & dirt + incoming lightning) |
| `test_autopause_alive_zero.JSON` | Simulation auto-pauses when `alive_count == 0` (all particles have `lifetime=2`) |

---

### Integration

| Test File | Requirement Tested |
|:---|:---|
| `test_all_types_integration.JSON` | One of every particle type in a 30×30 world — smoke test for the full system |

---

## JSON Format Notes

The parser (`extractParticle` in `World.cc`) reads fields by index after splitting on commas:

| Index | Field |
|:---:|:---|
| 0 | `row` |
| 1 | `col` |
| 2 | `x_vel` |
| 3 | `y_vel` |
| 4 | `r` |
| 5 | `g` |
| 6 | `b` |
| 7 | `stationary` |
| 8 | `lifetime` |
| 9 | `type` |

> **Note:** `r`/`g`/`b` values are saved but **not loaded** — those lines in `extractParticle` are commented out. Constructor defaults are used instead. Values are included in test files for format correctness.
>
> Trailing commas after each field (including the final `type` field) match the `save()` output format.
