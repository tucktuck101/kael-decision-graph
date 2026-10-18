# Kael's Decision Flowchart (v2.5)

Every path ends in one of the five punchlines (E1–E5). Combat is shared, but Kael's
intent is fixed when he enters it (`08 - …` nodes) and `Resume combat objective`
routes back to the outcomes for that intent only. With several opponents, each keeps the
intent they would get one-on-one and resolves through their own outcomes.

Party members have a relationship score from -5 to +5, starting at 0: cockblock -2,
annoyance -1, favour +1, wingman +2, saving his life +5, each week without a new strike +1 (capped at +5).
It is checked whenever the graph deals with that party member.
A possible child of Kael's (princess or prince) who is an adult party member starts at +5.

```mermaid
flowchart TD
    %% ================= WALKER RULES (ignored by Mermaid; read by index.html) =================
    %% Combat intent is set on entry and used by "Resume combat objective"
    %% @set KILLINTENT intent=Fight to kill
    %% @set MONSTERINTENT intent=Destroy it
    %% @set GRUDGEINTENT intent=Party member grudge
    %% @set SPAREINTENT intent=Spare her
    %% @set PARTNERINTENT intent=Spare her partner
    %% @set DEFENDINTENT intent=Defend and reconcile
    %% @dispatch MODE intent
    %% Who Kael is dealing with, used by "Who were they?"
    %% @start who=Anyone else
    %% @set PSCORE who=Party member
    %% @set MINORHOST who=Minor
    %% @set MRECON who=Minor
    %% @dispatch DPARTY who
    %% Party score tracker
    %% @event "Cockblock" -2
    %% @event "Annoyance" -1
    %% @event "Favour" +1
    %% @event "Wingman" +2
    %% @event "Saved his life" +5
    %% @event "Quiet week" +1
    %% @max 5
    %% @target PRINCESSSTART start=5
    %% @target PSCORE
    %% @score PMINUS -1 target
    %% @score PPLUS +1 target
    %% @score PHIT -5 target
    %% @score HUNTPLUS +1 target
    %% @score DRAGGED =-4 target
    %% @score WINGPLUS +2 pick
    %% @score HEALERPLUS +5 pick
    %% @score RESCUERPLUS +1 pick
    %% @check PCHECK "-5 or lower" <=-5
    %% @check PCHECK "-4 to +5" >=-4
    %% @check PBEST "Yes" ==5
    %% @check PBEST "No" <5
    %% @check HITCHECK "Yes" <=-5
    %% @check HITCHECK "No" >-5
    %% @check STILLGRUDGE "Yes" <=-5
    %% @check STILLGRUDGE "No, he cools off" >-5

    %% ================= NODES =================
    subgraph S_ENCOUNTER["01-02 · Encounter"]
        START(["Kael encounters a creature"])
        ALIVE{"01 - Is it alive?"}
        UH{"Is it hostile?"}
        NEED{"Does it need killing?"}
        HUM{"Is it humanoid?"}
        NH{"Is it hostile?"}
        PERFORMANCE{"Would people find it cute or interesting in a performance?"}
        TRAIN["Catch and train it"]
        FOOD{"Is it food?"}
        FEMALE{"Does it look female?"}
        CHILD{"Could they be Kael's child?"}
        DAUGHTERPARTY{"Are they a party member?"}
        DMINOR{"Still a minor?"}
        PRINCESSSTART["Party royalty: their score started at +5"]
        CHILDKILL{"Are they trying to kill him?"}
        KMINOR{"Are they a minor?"}
        ROYAL{"Son or daughter?"}
        PRINCESS["Treat her like a princess. Forever."]
        PRINCE["Treat him like a prince. Forever."]
        AGE{"Age group?"}
        PM{"02 - Is she a party member?"}
        FIRST{"First meeting?"}
        PELDER{"Is she elderly?"}
        ELDERQ{"Is she elderly?"}
        DEADPARTY{"Party member?"}
        BEASTPARTY{"Party member?"}
    end

    subgraph S_TASTE["03 · Taste check"]
        BODY{"03 - What's her body type?"}
        GOD["God damn!"]
        EYES["Struggles to maintain eye contact"]
        NOTUSUAL["Not my usual, but..."]
        ALT{"Alternative aesthetic, tattoos or piercings?"}
        HOT["Damn, she's hot."]
        DOM{"Strong or dominant personality?"}
        MOM["....Mommy?"]
        BOTH{"Both aesthetic and personality preferences?"}
        GOOD["I'll be a good boy... unless you don't want me to?"]
        TASTEDONE{"Party member?"}
    end

    subgraph S_WOMAN["04-05 · Approaching her"]
        WOMANHOST{"04 - Is she hostile?"}
        EMP{"Is she his employer?"}
        RISK{"Did she hit BOTH his aesthetic and personality preferences?"}
        MONEY["Need the money to flirt with other women"]
        MET{"Has he met her before?"}
        INTRO["Introduce himself"]
        CALM["05 - Try calming her down"]
        CW{"Did it work?"}
        GROVEL["Grovel"]
        GW{"Did it work?"}
        HARDER["Flirt harder"]
        HW{"Did it work?"}
        ESCALATE{"Is she physically attacking him now?"}
    end

    subgraph S_ROMANCE["11-13 · Romance"]
        INIT{"Did she initiate flirting?"}
        SUSPECT["Why the hell is she interested in ME?"]
        RELSTATUS{"Does she seem partnered?"}
        NEAR{"13 - Is her partner nearby?"}
        THREAT{"Could her partner kill Kael?"}
        CARE{"Does her partner care?"}
        SUBTLE["Flirt subtly"]
        HOWFLIRT{"Is she elderly?"}
        TASTEFUL["Flirt tastefully"]
        FLIRT["11 - Flirt openly or reciprocate"]
        PATTACK{"Does her partner attack Kael?"}
        COCKBLOCK{"Did a party member cockblock him?"}
        WINGMAN{"Did a party member act as his wingman?"}
        WINGPLUS["+2 to the wingman's score"]
        RESPONSE{"Did she respond positively?"}
        ELDERREJECT{"Elderly woman?"}
        RESPECT["Keep flirting respectfully without expectations"]
        PANIC["12 - PANIC!"]
        TRAP{"Is it a trap?"}
        PROBABLY["It's probably a trap"]
    end

    subgraph S_SOCIAL["04, 06, 10 · Hostility and reconciliation"]
        PSCORE["Update their relationship score: cockblock -2, annoyance -1, favour +1, wingman +2, saved his life +5, each quiet week +1"]
        PCHECK{"Relationship score?"}
        PARTYHOST{"Is this party member hostile?"}
        PANNOY{"Are they annoying him?"}
        PBEST{"Score at +5?"}
        PMINUS["-1 to their score"]
        UMOCK["Cast Vicious Mockery"]
        OPARTY{"Party member?"}
        OTHERHOST{"04 - Are they hostile?"}
        ACTIVELY{"Trying to kill Kael?"}
        BENEFIT{"Kael's fault or beneficial relationship?"}
        STRONG{"Likely stronger than Kael?"}
        MIGHTKILL{"Might they kill him?"}
        PREMOCK["Cast Vicious Mockery first"]
        ATTACK["Attack"]
        FRIEND{"10 - Advantage to befriending them?"}
        POLITE["Be polite"]
        SOCIALMOCK["Cast Vicious Mockery"]
        PRECON["06 - Try to patch things up"]
        PRR{"How do they respond?"}
        PPLUS["+1 to their score"]
        PHARDER["Try harder"]
        PHIT["-5 to their score"]
        HITCHECK{"Score now -5 or lower?"}
        DPARTY{"Who were they?"}
        MINORHOST{"Is the kid hostile?"}
        MRECON["06 - Try to make peace with the kid"]
        MRR{"How does the kid respond?"}
        MAGE{"Is he a minor?"}
        MHARDER["Try harder"]
        RECON["06 - Try resolving the conflict"]
        RR{"How do they respond?"}
        RB{"Relationship beneficial?"}
        SAVE{"Relationship worth saving?"}
        HARDRECON["Try harder"]
        CANKILL{"Can Kael defeat them?"}
        STILLWORTH{"Still worth saving?"}
        WAIT["Wait a period of time"]
        STILLHOST{"Still hostile?"}
        IMPROVED{"Relationship improved?"}
        ATTACKING{"Actively attacking Kael?"}
        NOWWIN{"Can Kael defeat them now?"}
    end

    subgraph S_COMBAT["07-09 · Combat"]
        KILLINTENT["08 - Fight to kill"]
        MONSTERINTENT["08 - Destroy it"]
        GRUDGEINTENT["08 - Fight them to the death"]
        SPAREINTENT["08 - Try not to kill her"]
        PARTNERINTENT["08 - Try not to kill her partner"]
        DEFENDINTENT["08 - Defend without abandoning reconciliation"]

        BATTLE["Enter combat (each opponent keeps their own intent)"]
        LETHAL{"07 - Potentially lethal?"}
        DYING{"Is Kael about to die?"}
        SURVPANIC["PANIC!"]
        SELF{"Can he heal himself?"}
        HEAL["Heal himself"]
        OTHERS{"Can anyone else heal?"}
        BEGHELP["Beg for help"]
        HEALED{"Did they heal him?"}
        HEALERPARTY{"Was it a party member?"}
        HEALERPLUS["+5 to the healer's score. He owes them his life."]
        MERCY["Beg for mercy"]
        MW{"Did it work?"}
        SERVANT["Feign servitude and seek escape"]
        MODE{"Resume combat objective"}

        COMBATOUT{"Combat outcome?"}
        SURRENDER{"Relationship worth saving?"}
        ACCEPT["Accept surrender"]
        FLEE{"Reason to kill them?"}
        PURSUE["Pursue them"]
        CAUGHT{"Caught them?"}
        KEEPLOOKING{"Need to keep looking?"}

        MONOUT{"Combat outcome?"}

        GRUDGEOUT{"Combat outcome?"}
        NOMERCY["Surrender? Keep swinging."]
        HUNT["Hunt them down"]
        UCAUGHT{"Caught them?"}
        HUNTWEEK{"A week gone without finding them?"}
        HUNTPLUS["+1 to their score"]
        STILLGRUDGE{"Still -5 or lower?"}
        COOLED["Eh. They're not worth the boots."]
        DRAGGED["Dragged away, still fuming. Score back to -4"]
        RESCUERPLUS["+1 to the rescuer's score (a favour)"]

        SPAREOUT{"09 - How does the fight end?"}
        ACCEPTHER["Accept her surrender"]
        AGAIN["Try flirting again"]
        LETGO["Let her go"]
        KILLER{"Who killed her?"}
        GUILT["Guilty about losing his chance at love"]
        ANNOYED["Quietly annoyed with them"]
        WHOANNOY{"Annoying party member?"}

        PARTNEROUT{"How does the fight with her partner end?"}
        MOODKILL["Well, that ruined the mood"]
        PKILLER{"Who killed her partner?"}
        SINGLE["Well... she's single now."]

        DEFENDOUT{"How does the fight end?"}
        COOLOFF["Give them time to cool off"]
    end

    subgraph S_ENDINGS["Endings"]
        E1(["E1 - KEEP FLIRTING, IT MIGHT STILL WORK"])
        E2(["E2 - PREPARE NEW CHARACTER SHEET"])
        E3(["E3 - NEW BESTIE!"])
        E4(["E4 - KILL THEM"])
        E5(["E5 - TOLERATE THEM"])
    end

    %% ================= EDGES =================
    %% --- Encounter ---
    START --> ALIVE
    ALIVE -->|No| DEADPARTY
    DEADPARTY -->|Yes| PSCORE
    DEADPARTY -->|No| UH
    UH -->|Yes| MONSTERINTENT
    UH -->|No| NEED
    NEED -->|Yes| MONSTERINTENT
    NEED -->|No| E5

    ALIVE -->|Yes| HUM
    HUM -->|No| BEASTPARTY
    BEASTPARTY -->|Yes| PSCORE
    BEASTPARTY -->|No| NH
    NH -->|Yes| MONSTERINTENT
    NH -->|No| PERFORMANCE
    PERFORMANCE -->|Yes| TRAIN
    TRAIN --> E3
    PERFORMANCE -->|No| FOOD
    FOOD -->|Yes| MONSTERINTENT
    FOOD -->|No| E5

    HUM -->|Yes| CHILD
    CHILD -->|No| FEMALE
    FEMALE -->|No| MAGE
    MAGE -->|Yes| MINORHOST
    MAGE -->|No| OPARTY
    OPARTY -->|Yes| PSCORE
    OPARTY -->|No| OTHERHOST
    FEMALE -->|Yes| AGE
    CHILD -->|Yes| DAUGHTERPARTY
    DAUGHTERPARTY -->|Yes| DMINOR
    DMINOR -->|No| PRINCESSSTART
    PRINCESSSTART --> PSCORE
    DMINOR -->|Yes| CHILDKILL
    DAUGHTERPARTY -->|No| CHILDKILL
    CHILDKILL -->|No| ROYAL
    ROYAL -->|Daughter| PRINCESS
    ROYAL -->|Son| PRINCE
    PRINCESS --> E3
    PRINCE --> E3
    CHILDKILL -->|Yes| KMINOR
    KMINOR -->|Yes, defend only| MRECON
    KMINOR -->|No, normal hostile rules| OTHERHOST
    AGE -->|Minor| MINORHOST
    MINORHOST -->|"No (meeting them again as an adult is a new encounter)"| E5
    MINORHOST -->|Yes| MRECON
    MRECON --> MRR
    MRR -->|Hostility ends| E5
    MRR -->|Still hostile| MHARDER
    MHARDER --> MRECON
    MRR -->|Physically attacks, defend only| DEFENDINTENT
    AGE -->|Adult| PM
    AGE -->|Elder| PM

    PM -->|Yes| FIRST
    FIRST -->|Yes| PELDER
    PELDER -->|Yes| PSCORE
    PELDER -->|No| BODY
    FIRST -->|No| PSCORE
    PM -->|No| ELDERQ
    ELDERQ -->|Yes| WOMANHOST
    ELDERQ -->|No| BODY

    %% --- Taste check ---
    BODY -->|Thicc or athletic| GOD
    BODY -->|Busty or curvy| EYES
    BODY -->|Plus-size, petite, slim or muscular| NOTUSUAL
    GOD --> ALT
    EYES --> ALT
    NOTUSUAL --> ALT
    ALT -->|Yes| HOT
    ALT -->|No| DOM
    HOT --> DOM
    DOM -->|Yes| MOM
    DOM -->|No| BOTH
    MOM --> BOTH
    BOTH -->|Yes| GOOD
    BOTH -->|No| TASTEDONE
    GOOD --> TASTEDONE
    TASTEDONE -->|Yes, no flirting| PSCORE
    TASTEDONE -->|No| WOMANHOST

    %% --- Approaching her ---
    WOMANHOST -->|No| EMP
    WOMANHOST -->|Just angry| CALM
    WOMANHOST -->|Trying to kill him| SPAREINTENT
    EMP -->|No| MET
    EMP -->|Yes| RISK
    RISK -->|Yes, worth risking income and reputation| MET
    RISK -->|No| MONEY
    MONEY --> E5
    MET -->|No| INTRO
    MET -->|Yes| INIT
    INTRO --> INIT

    CALM --> CW
    CW -->|Yes| E1
    CW -->|No| GROVEL
    GROVEL --> GW
    GW -->|Yes| E1
    GW -->|No| HARDER
    HARDER --> HW
    HW -->|Yes| E1
    HW -->|No| ESCALATE
    ESCALATE -->|Yes| SPAREINTENT
    ESCALATE -->|No| CALM

    %% --- Romance ---
    INIT -->|Yes| SUSPECT
    INIT -->|No| RELSTATUS
    SUSPECT --> RELSTATUS
    RELSTATUS -->|No| HOWFLIRT
    RELSTATUS -->|Yes| NEAR
    NEAR -->|No| HOWFLIRT
    NEAR -->|Yes| THREAT
    THREAT -->|No| HOWFLIRT
    THREAT -->|Yes| CARE
    CARE -->|No| HOWFLIRT
    CARE -->|Yes| SUBTLE
    HOWFLIRT -->|Yes| TASTEFUL
    HOWFLIRT -->|No| FLIRT
    SUBTLE --> PATTACK
    TASTEFUL --> PATTACK
    FLIRT --> PATTACK
    PATTACK -->|Yes| PARTNERINTENT
    PATTACK -->|No, or no partner| COCKBLOCK
    COCKBLOCK -->|Yes, flirting is over. Turn on the cockblocker| PSCORE
    COCKBLOCK -->|No| WINGMAN
    WINGMAN -->|Yes| WINGPLUS
    WINGPLUS --> RESPONSE
    WINGMAN -->|No| RESPONSE
    RESPONSE -->|Yes| PANIC
    RESPONSE -->|No| ELDERREJECT
    ELDERREJECT -->|Yes| RESPECT
    ELDERREJECT -->|No| E1
    RESPECT --> E1
    PANIC --> TRAP
    TRAP -->|Yes| E1
    TRAP -->|No| PROBABLY
    PROBABLY --> E1

    %% --- Hostility and reconciliation ---
    PSCORE --> PCHECK
    PCHECK -->|"-5 or lower"| UMOCK
    UMOCK --> GRUDGEINTENT
    PCHECK -->|"-4 to +5"| PARTYHOST
    PARTYHOST -->|No| PANNOY
    PANNOY -->|Yes| PMINUS
    PMINUS --> PSCORE
    PANNOY -->|No| PBEST
    PBEST -->|Yes| E3
    PBEST -->|No| E5
    PARTYHOST -->|Yes| PRECON
    PRECON --> PRR
    PRR -->|Made up| PPLUS
    PPLUS --> PSCORE
    PRR -->|Hostility ends without making up| E5
    PRR -->|Still hostile| PHARDER
    PHARDER --> PRECON
    PRR -->|Physically attacks| PHIT
    PHIT --> HITCHECK
    HITCHECK -->|Yes| UMOCK
    HITCHECK -->|No| DEFENDINTENT

    OTHERHOST -->|No| FRIEND
    OTHERHOST -->|Yes| ACTIVELY
    ACTIVELY -->|Yes| KILLINTENT
    ACTIVELY -->|No| BENEFIT
    BENEFIT -->|Yes| RECON
    BENEFIT -->|No| STRONG
    STRONG -->|Yes| WAIT
    STRONG -->|No| MIGHTKILL
    MIGHTKILL -->|Yes| PREMOCK
    MIGHTKILL -->|No| ATTACK
    PREMOCK --> KILLINTENT
    ATTACK --> KILLINTENT

    FRIEND -->|Yes| E3
    FRIEND -->|No| POLITE
    POLITE --> SOCIALMOCK
    SOCIALMOCK --> KILLINTENT

    RECON --> RR
    RR -->|Reconciled| RB
    RB -->|Yes| E3
    RB -->|No| E5
    RR -->|Hostility ends without friendship| E5
    RR -->|Still hostile| SAVE
    SAVE -->|Yes| HARDRECON
    HARDRECON --> RECON
    SAVE -->|No| CANKILL
    CANKILL -->|Yes| PREMOCK
    CANKILL -->|No| WAIT
    RR -->|Physically attacks| STILLWORTH
    STILLWORTH -->|Yes| DEFENDINTENT
    STILLWORTH -->|No| KILLINTENT

    WAIT --> STILLHOST
    STILLHOST -->|No| IMPROVED
    IMPROVED -->|Yes| E3
    IMPROVED -->|No| E5
    STILLHOST -->|Yes| ATTACKING
    ATTACKING -->|Yes| KILLINTENT
    ATTACKING -->|No| NOWWIN
    NOWWIN -->|Yes| PREMOCK
    NOWWIN -->|No| WAIT

    %% --- Combat: intent is fixed on entry ---
    KILLINTENT --> BATTLE
    MONSTERINTENT --> BATTLE
    GRUDGEINTENT --> BATTLE
    SPAREINTENT --> BATTLE
    PARTNERINTENT --> BATTLE
    DEFENDINTENT --> BATTLE

    BATTLE --> LETHAL
    LETHAL -->|No| MODE
    LETHAL -->|Yes| DYING
    DYING -->|No| MODE
    DYING -->|Yes| SURVPANIC
    SURVPANIC --> SELF
    SELF -->|Yes| HEAL
    HEAL --> MODE
    SELF -->|No| OTHERS
    OTHERS -->|Yes| BEGHELP
    BEGHELP --> HEALED
    HEALED -->|Yes| HEALERPARTY
    HEALERPARTY -->|Yes| HEALERPLUS
    HEALERPLUS --> MODE
    HEALERPARTY -->|No| MODE
    HEALED -->|No| E2
    OTHERS -->|No| MERCY
    MERCY --> MW
    MW -->|No| E2
    MW -->|Yes| SERVANT
    SERVANT --> E5

    MODE -->|Fight to kill| COMBATOUT
    MODE -->|Destroy it| MONOUT
    MODE -->|Party member grudge| GRUDGEOUT
    MODE -->|Spare her| SPAREOUT
    MODE -->|Spare her partner| PARTNEROUT
    MODE -->|Defend and reconcile| DEFENDOUT

    %% Fight to kill (humanoids)
    COMBATOUT -->|Opponent killed| E4
    COMBATOUT -->|Kael dies| E2
    COMBATOUT -->|Opponent surrenders or is incapacitated| SURRENDER
    COMBATOUT -->|Opponent flees| FLEE
    COMBATOUT -->|Fight continues| BATTLE
    SURRENDER -->|Yes| ACCEPT
    ACCEPT --> RECON
    SURRENDER -->|No| E4
    FLEE -->|No| E5
    FLEE -->|Yes| PURSUE
    PURSUE --> CAUGHT
    CAUGHT -->|Yes| BATTLE
    CAUGHT -->|No| KEEPLOOKING
    KEEPLOOKING -->|Yes| PURSUE
    KEEPLOOKING -->|No| E5

    %% Destroy it (monsters, undead, food): no reconciliation
    MONOUT -->|Destroyed, surrenders or incapacitated| E4
    MONOUT -->|Kael dies| E2
    MONOUT -->|It flees| FLEE
    MONOUT -->|Fight continues| BATTLE

    %% Party member grudge: to the death
    GRUDGEOUT -->|They die| E4
    GRUDGEOUT -->|Kael dies| E2
    GRUDGEOUT -->|They surrender or are incapacitated| NOMERCY
    NOMERCY --> BATTLE
    GRUDGEOUT -->|They flee| HUNT
    GRUDGEOUT -->|Another party member drags Kael away| DRAGGED
    DRAGGED --> RESCUERPLUS
    RESCUERPLUS --> E5
    GRUDGEOUT -->|Fight continues| BATTLE
    HUNT --> UCAUGHT
    UCAUGHT -->|Yes| BATTLE
    UCAUGHT -->|No| HUNTWEEK
    HUNTWEEK -->|No| HUNT
    HUNTWEEK -->|Yes| HUNTPLUS
    HUNTPLUS --> STILLGRUDGE
    STILLGRUDGE -->|Yes| HUNT
    STILLGRUDGE -->|No, he cools off| COOLED
    COOLED --> E5

    %% Spare her
    SPAREOUT -->|She surrenders or is incapacitated| ACCEPTHER
    ACCEPTHER --> AGAIN
    AGAIN --> INIT
    SPAREOUT -->|She retreats| LETGO
    LETGO --> E1
    SPAREOUT -->|Kael dies| E2
    SPAREOUT -->|Fight continues| BATTLE
    SPAREOUT -->|She dies| KILLER
    KILLER -->|Kael accidentally| GUILT
    GUILT --> E4
    KILLER -->|Someone else| ANNOYED
    ANNOYED --> WHOANNOY
    WHOANNOY -->|Yes| E5
    WHOANNOY -->|No| E3

    %% Spare her partner
    PARTNEROUT -->|Partner surrenders, flees or is incapacitated| AGAIN
    PARTNEROUT -->|Partner dies| PKILLER
    PKILLER -->|Kael| MOODKILL
    PKILLER -->|Someone else| SINGLE
    SINGLE --> AGAIN
    MOODKILL --> E4
    PARTNEROUT -->|Kael dies| E2
    PARTNEROUT -->|Fight continues| BATTLE

    %% Defend and reconcile
    DEFENDOUT -->|Safely disengaged| DPARTY
    DEFENDOUT -->|They surrender or are incapacitated| DPARTY
    DEFENDOUT -->|They flee| COOLOFF
    COOLOFF --> DPARTY
    DPARTY -->|Party member| PRECON
    DPARTY -->|Minor| MRECON
    DPARTY -->|Anyone else| RECON
    DEFENDOUT -->|Kael accidentally kills them| E4
    DEFENDOUT -->|Kael dies| E2
    DEFENDOUT -->|Fight continues| BATTLE

    %% ================= STYLES =================
    classDef ending fill:#e6f4e8,stroke:#35945b,color:#164e30,stroke-width:2px
    classDef monologue fill:#fff4d6,stroke:#c99a2e,color:#5a3d00,stroke-width:2px
    classDef intent fill:#fde8e8,stroke:#c0392b,color:#6b1a12,stroke-width:2px
    class E1,E2,E3,E4,E5 ending
    class GOD,EYES,NOTUSUAL,HOT,MOM,GOOD,MONEY,SUSPECT,PANIC,PROBABLY,SURVPANIC,NOMERCY,MOODKILL,GUILT,ANNOYED,DRAGGED,COOLED,SINGLE monologue
    class KILLINTENT,MONSTERINTENT,GRUDGEINTENT,SPAREINTENT,PARTNERINTENT,DEFENDINTENT intent
```
