DRAFT SOLVER — USER-FRIENDLY CHANGELOG
Current build: v21.10.0.1

This is a condensed version of the changelog embedded in the app. Internal implementation notes, maintainer documentation, test-harness updates, and changes with no effect on normal use have been omitted unless they explain an important fix.


FOUNDATIONS — v2.0 to v3.3

• Expanded and separated the manager database, improved manager selection, and added clearer substitution guidance.
• Added accent-insensitive searching and improved dropdown behavior on mobile.
• Made incomplete or difficult boards fail gracefully by filling as much of the squad as possible.
• Rebuilt the app around the full formation-based draft board, including starters, bench slots, captain selection, holds, commits, and busts.
• Added the pick helper, chemistry-aware card evaluation, rarity controls, and emergency out-of-position filling.
• Added database tools for players and managers, edit mode, import/export, reset controls, and automatic local saving.


SOLVER RELIABILITY AND RATING CEILING — v8.12 to v10.1

• Fixed cases where the displayed XI, saved recreation log, manager analysis, and exported result could disagree about where players were placed.
• Improved relayout logic so solved squads use fewer unnecessary player moves while preserving the same score and chemistry.
• Added clearer Rating Ceiling feedback so users can tell whether a ceiling may have hidden a better squad.
• Replaced search-dependent ceiling estimates with a safe calculated upper bound.
• Added “Optimal RC”, allowing the app to automatically choose the tightest safe Rating Ceiling for faster searches.
• Added “Skip ties”, which can ignore equal-scoring alternatives and search only for a strictly better score.
• Improved same-name card disambiguation in Pick per hold, including cards with matching names, ratings, types, or positions.
• Added chemistry-overlap information and an all-fresh bonus to helper evaluations.
• Expanded advanced rating thresholds to support ratings above 99 and lower-rating events.
• Widened the Rating Ceiling range down to 75 for unusually low-rated drafts.


SEARCH CONTROL AND DIVERSITY — v11 to v12

• Improved candidate ordering so capped searches are more likely to find a stronger squad before the node limit is reached.
• Added separate node caps for the main solver, helper, bench analysis, and manager analysis.
• Added Search diversity, which divides the same search budget between the normal best-first order and shuffled restart passes.
• Fixed diversity searches losing tied squads.
• Replaced fixed diversity presets with direct controls for the normal-search percentage and number of shuffled passes.
• Improved Full random mode by using many independent attempts instead of one long random traversal.
• Tightened several search bounds, reducing wasted work without changing valid results.


OBJECTIVE HELPER CALIBRATION — v13

• Added optional DB-calibrated helper weights. The helper can now learn card-value factors from simulated drafts using the active database instead of relying only on manually tuned weights.
• Added calibration controls for the number of simulated drafts and the random seed.
• Made large calibration runs yield to the browser so the page remains responsive.
• Added a visible Uncalibrate option to return to manual helper weights.
• Fixed calibration persistence, stale-state handling, and several misleading helper warnings.
• Improved the emergency out-of-position solver so it respects the same relevant search settings as the main solver.


PARALLEL SEARCH — v14

• Added multi-worker parallel searching for large drafts.
• Added a Stop button for worker-based searches and a configurable worker count.
• Added parallel-search information to recreation logs and saved settings.
• Removed the beta label after the parallel path had been tested and stabilized.


FORMATION AND BENCH CALIBRATION — v15

• Added an objective Formation Calibrator to rank formations from the available player pool instead of relying on a manually tuned position-weight grid.
• Allowed Formation Calibration to automatically run the card-weight calibration it needs, avoiding a setup dead end.
• Added an objective bench-value option.
• Fixed the slow bench tiers so their intended search depth is actually guaranteed.


MULTI-LEAGUE, PIVOTS, CHEMISTRY, AND MAJOR SPEED WORK — v16

• Generalized the app beyond a Premier-League-only normal-card database. Normal cards now use their real league, club, and primary-position data.
• Added real primary-position support throughout formation analysis and database entries.
• Fixed full-chem scoring on mixed-league squads and added per-player chemistry indicators in the solved XI.
• Generalized freshness, rarity, common-league, and helper logic for league and nation pivots.
• Expanded the Pivot Analyzer to support both league and nation pivots and allowed either kind to become the active helper pivot.
• Replaced the old Pivot “ceiling” with a true upper bound and kept the concrete buildable squad as a separate lower figure.
• Added multi-league test cards and improved league/club handling in the Add card form.
• Made calibration copy-aware, so cards with multiple copies are sampled more often.
• Fixed stale calibration messages after database resets or changes.
• Added several major solver pruning improvements, dramatically reducing the work required on large drafts.
• Added slot-symmetry pruning so interchangeable formation slots are not searched in every equivalent order.
• Made Skip ties default to ON, while still allowing users to turn it off to browse equal-scoring squads.
• Made Parallel search default to OFF because the improved serial solver became fast enough for most normal drafts.


HELPER, DATABASE, STOP BUTTON, AND LARGE-SEARCH QUALITY — v17

• Refined pivot-aware helper scoring so strong off-pivot cards are not unfairly blocked while committed pivots still receive appropriate support.
• Added clearer pivot mismatch, top-evaluation, and recalibration warnings.
• Made Pivot Analyzer run automatically at startup.
• Added full nation/league/club chemistry badges to helper rows and clearer pick-time coverage messages.
• Added calibrated rarity effects and separate controls for pivot normals versus Icons/Heroes.
• Improved the Weights tab layout with collapsible sections and shorter labels.
• Fixed database import/edit paths so copies, primary position, and identity data are preserved.
• Added editable identity support through pidx, allowing different real players with the same displayed name to remain separate.
• Changed formation analysis to recognize one real player who has card versions with different primary positions.
• Added and corrected several Premier League and Icon database entries.
• Added live progress and a working Stop button for deep main searches.
• Made stopped searches keep the best result found so far and base “Keep searching x3” on the work actually completed.
• Moved bench and manager analysis into a worker with its own live node count and Stop button.
• Added worker-backed stopping for single-tie re-analysis and emergency out-of-position searches.
• Integrated concise deadweight suggestions into the oversized-board warning.
• Removed repeated “this could take forever” confirmation dialogs; long searches remain explicit user actions.


RESUMABLE SEARCH, PARALLEL BENCH, AND MAJOR DATABASE EXPANSION — v18

Search and resume:
• Added checkpoint-based continuation for stopped searches on the beta branch.
• Extended continuation to parallel main searches, with one verified frontier per worker partition.
• Made saved frontiers survive reloads when they are small enough to store safely.
• Hardened immediate Stop, repeated Stop, cap-trip, reload, and worker-layout cases so saved progress does not move backward or silently restart completed work.
• Kept the best previously displayed XI when a resumed rung temporarily reports a weaker partial result.
• Added safe “Keep searching x3” calculations based on actual explored nodes while separately showing the safe checkpoint total.

Bench and manager analysis:
• Added parallel exhaustive bench analysis.
• Allowed one extremely large bench tie to be divided into exact non-overlapping worker ranges.
• Treated the Bench Node Cap as one total budget shared across active workers.

Pivot and calibration:
• Changed Pivot ranking to prioritize a real buildable XI, then supply, with ceiling used only as a final tiebreak.
• Added supply-aware and diversity-aware penalties so very thin pivots no longer look unrealistically strong.
• Added compact advanced settings for pivot exposure, supply penalties, and diversity.
• Reworked rarity calibration to fit separate nation, club, and league effects objectively.
• Added independently fitted Icon and Hero value.
• Raised automatic calibration size and enforced a minimum sample count to avoid misleading tiny calibrations.

Database and usability:
• Imported large FC 26 and PACWYN card batches, including men’s 75+ cards outside the original Premier League pool, WSL cards, Golden Ball, Swaps, TOTS, Path to Glory, Pro Leagues, Pro Live, National Pride, and other special collections.
• Added more league aliases and country/adjective search support, including women’s leagues.
• Added partial name + rating manager search.
• Improved database action layout and several card/nation/club corrections.


CLEAN DATABASE REBUILD AND CALIBRATOR FIXES — v19

Database rebuild:
• Rebuilt the database from clean source JSON files instead of continuing the older incremental database.
• Added complete Premier League normals, Heroes, Icons, and then progressively rebuilt many additional men’s and women’s leagues.
• Expanded the embedded database to more than 10,000 unique rows and over 10,400 cards including copies.
• Added or completed leagues including Serie A/Serie B, Eredivisie, Belgian Pro League, UAE Pro League, Scottish Premiership, Greece Super League, several women’s leagues, Croatia, Sweden, Australia, Poland, Romania, Azerbaijan, Cyprus, Libertadores, and others.
• Added canonical nation and league naming fixes and removed stale aliases.
• Switched duplicate-player handling to real-person identity using displayed name plus pidx, regardless of changes in rating, nation, club, league, type, or position.
• Added pidx fields to the Add and Edit card forms.
• Restored several missed cards and corrected misplaced club blocks.
• Added an Argentina historical set and the Chenzo 105 Yugoslavia goalkeeper card.

Pivot Analyzer and UI:
• Reworked Pivot Analyzer Advanced settings into a compact layout with shorter labels and a penalty preview.
• Made Pivot analysis run automatically after the page loads.
• Added a visible stale warning whenever the player database changes after the last analysis.

Calibration and formation fixes:
• Fixed helper calibration so it trains on the active pivot pool rather than unrelated normals from the entire multi-league database.
• Added the best simulated score and a score-frequency breakdown to calibration results.
• Included the manager bonus in displayed simulated final scores.
• Fixed rarity calculations so Icons, Heroes, and pivot normals are compared against the same relevant pool.
• Fixed the Formation Calibrator silently falling back to the old Gold database.
• Made the live database authoritative whenever usable primary-position data exists.
• Added a normals-only Formation Calibrator comparison before the later v20 redesign.


FORMATION CALIBRATOR REWORK — v20

• Replaced the previous formation-calibration dependency with a simpler model based on the active pivot’s normal cards.
• Ranked players using rating plus capped rarity value, preventing low-rated rarity outliers from overtaking elite cards.
• Added persistent Advanced controls for formation depth, rarity curves, and commonness penalties.
• Improved helper calibration sampling so thin pivots do not create unrealistic squads dominated by Icons and Heroes.
• Prevented repeated calibration clicks from starting overlapping runs and invalidated incompatible old calibration results.


FORMATION SIMULATOR AND MODERN PIVOT ANALYZER — v21

v21.0–v21.1 — Formation simulation
• Replaced analytic Formation weights with seeded draft simulations for every formation.
• Starter offers now require exact primary-position matches and use shared position packs for fair comparisons.
• Simulations prevent duplicate real people and use a realistic mix of normals, Heroes, and Icons.
• Formation results show average, best, and worst final scores.
• Ranking blends average performance, upside, and reliability instead of using one extreme result.

v21.2–v21.5 — Pivot scores made more honest
• Stopped modifying the concrete buildable score with hidden penalty curves.
• Separated the best concrete squad from the score a pivot is expected to hit consistently.
• Reworked the displayed figures into Consistent, High Score, and Theoretical Max.
• Ranked pivots by Consistent score, which considers typical best-to-average drop, supply depth, and concentration within the pivot.
• Added clearer supply figures showing unique players and copies-weighted total supply.
• Expanded the list to the top 10 pivots and redesigned each result into a compact two-line card.
• Version changes now invalidate old calibration results instead of silently reusing them.

v21.6 — Reliability
• Replaced the old 55-card board-coverage gate with a direct XI-buildability check.
• A pivot is now considered viable when its distinct normal players can cover enough real formation slots and global Heroes/Icons can legally complete the XI.
• This stopped goalkeeper-light but otherwise playable pivots from being rejected for the wrong reason.

v21.7–v21.8 — Advanced simulation mix and squad rules
• Lowered Pivot Analyzer entry requirements to the seven pivot normals actually needed by the scoring model.
• Added Advanced calibration controls for average Icon/Hero mix and random spread.
• Pivot simulations now use only pivot-matching normals plus global Icons and Heroes.
• Final simulated XIs require at least seven pivot normals by default and respect configurable Icon, Hero, and combined-special caps.
• Rejected simulations are counted, and a pivot reports failure when every simulation is rejected.
• Removed the read-only Normal-average field; the normal amount is calculated automatically from the remaining offer total.
• Allowed special caps up to 11 for deliberate special-heavy testing.
• Blocked pivot changes while a calibration run is active to prevent desynchronization.
• Moved helper calibration fully to the responsive asynchronous fitter so scrolling and navigation remain usable during a run.

v21.9 — Zeroed-type calibration
• Icon and Hero values now show “not measured” when that card type cannot be selected.
• Types set to zero no longer leak back into the simulation as positional fallback cards.
• League rarity and new-league effects are not fitted for league pivots when Heroes are unavailable, because those factors cannot be observed in that setup.

v21.10.0–v21.10.0.1 — Inter Milan database rebuild
• Rebuilt the complete Inter Milan normal-card section from the supplied screenshots.
• Restored missing historical Inter cards and Dumfries 96.
• Corrected positions and Bonny 95’s Ivory Coast nationality while retaining his France variant as the same real player.
• Kept only genuine card copies rather than screenshot overlap.
• Corrected the Saudi 97 card’s displayed name to Cristiano Ronaldo.
• Removed the unnecessary Ronaldo identity split because Cristiano Ronaldo and Brazilian Ronaldo already have different displayed names.
• Corrected the two Calhanoglu 89 screenshots as one genuine CDM/CM card with two copies; the apparent CAM position was a visual misread.
• Preserved the separate Maicon identities where needed.
• Current synchronized database: 10,080 unique rows / 10,495 expanded cards.


CURRENT BUILD SUMMARY — v21.10.0.1

The current app includes:
• A stoppable, resumable, parallel-capable squad solver.
• Objective helper and formation calibration.
• Primary-position formation simulations.
• League and nation Pivot Analyzer rankings with realistic supply and reliability handling.
• Editable player identities, copies, positions, leagues, clubs, and pidx values.
• A clean multi-league database with more than 10,000 unique card rows.
• The corrected and completed Inter Milan card block.

