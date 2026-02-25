
## Test Files → REQUIREMENTS Mapping

### Particle Physics (Requirement 1)

| Test File | Requirement Tested |
|---|---|
| `test_air_straight_line.JSON` | "Air moves in a straight line (ignoring gravity) bouncing off solid" — 3 air particles with different velocities |
| `test_dust_gravity_random.JSON` | "Dust has a small amount of gravity and randomly moves left and right every frame" — 3 dust particles in open space |
| `test_fire_spawns_lightning.JSON` | "Fire is stationary and shoots sparks of lightning in different directions over time" — lone fire particle |
| `test_water_gravity.JSON` | "Water drips down" — 3 water particles in open space, should fall |
| `test_water_slide.JSON` | "if it hits something solid it will slide sideways to find the lowest level" — water above earth platform |
| `test_water_fire_interaction.JSON` | "Water touching fire turns into air moving upwards" — water above fire |
| `test_water_fire_chain.JSON` | Full chain: multiple water drops falling toward fire at bottom |
| `test_earth_stationary.JSON` | "Earth is always stationary and solid" — row of earth blocks |
| `test_lightning_straight_line.JSON` | "Lightning travels in a straight line and stops when it hits something solid" |
| `test_lightning_water_interaction.JSON` | "If it touches water, the water turns into lightning" |
| `test_lightning_earth_to_dirt.JSON` | "If it hits earth it turns into dirt" |
| `test_dirt_pile.JSON` | "Dirt travels downwards and forms piles when it hits something solid" — dirt above earth platform |
| `test_water_pool_basin.JSON` | Water settling into U-shaped earth basin — tests full water flow behavior |
| `test_fire_earth_chain.JSON` | Fire → spawns lightning → lightning hits earth → earth becomes dirt (full chain) |

### World Class (Requirement 2)

| Test File | Requirement Tested |
|---|---|
| `test_boundary_deletion.JSON` | "Any point which leaves the boundary must be deleted" — 4 air particles flying toward each edge |
| `test_size_alive_count.JSON` | `World::size()` and `World::alive_count()` — mix of 5 particles with varying lifetimes |
| `test_save_load_roundtrip.JSON` | `World::save()` and `World::load()` — complex scene with all types for round-trip verification |
| `test_empty_world.JSON` | Edge case: empty particle list. Tests physics(), size(), alive_count() on empty |
| `test_duplicate_position.JSON` | "No two Particles can be on the same location" — two particles at (10,10) |

### Lifetime & Stationary (Requirements 1 subsections)

| Test File | Requirement Tested |
|---|---|
|`test_lifetime_decrement.JSON`| "Physics will decrement it each frame by 1" + "lifetime of exactly 0, delete it" — particles with lifetimes 1, 3, 5 + one earth with -1 |
| `test_stationary_behavior.JSON` | "stationary=true means it is solid and does not move" + "Stationary can still be transformed" — stationary water & dirt + incoming lightning |
| `test_autopause_alive_zero.JSON` | "Simulation should also automatically pause when world.alive_count is 0" — all particles have lifetime=2 |

### Integration

| Test File | Requirement Tested |
|---|---|
| `test_all_types_integration.JSON` | One of every particle type in a 30×30 world — smoke test for overall system |

## JSON Format Notes

The parser (`extractParticle` in World.cc) reads fields by index after splitting on commas:
- Index 0: row, 1: col, 2: x_vel, 3: y_vel, 4: r, 5: g, 6: b, 7: stationary, 8: lifetime, 9: type

**Important**: r/g/b values are saved but NOT loaded (those lines in `extractParticle` are commented out). The constructor defaults are used instead. The values are included in these files for format correctness.

Trailing commas after each field (including the last `type` field) match the save() output format.
