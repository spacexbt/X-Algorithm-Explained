# X Algorithm Explained (Simple English)

## What Is This?

X (formerly Twitter) open-sourced their "For You" feed algorithm in January 2026. This is how X decides which posts to show you — and more importantly for us, how it decides whether YOUR posts get seen by others.

The new system is called **Phoenix** and is powered by the same AI (Grok) that runs xAI's chatbot.

---

## The Core Idea

Every post competes for attention. The algorithm assigns each post a **score** based on how likely YOU (the viewer) are to engage with it. Higher score = shown to more people.

**The formula:**

```
Post Score = Σ (weight × probability of action)
```

Translation: The algorithm predicts how likely you are to like, reply, repost, etc. — then multiplies each prediction by how much X values that action.

---

## The Engagement Weights (This Is Gold)

Not all engagement is equal. Here's what X actually values:

| Action | Weight | What It Means |
|--------|--------|---------------|
| Reply that gets a reply back | **75x** | Conversations are king |
| You reply to a post | **13.5x** | Replies matter way more than likes |
| Profile click → like/reply | **12x** | Deep engagement signals |
| Click into thread + reply | **11x** | Thread participation |
| Stay in thread 2+ min | **10x** | Dwell time matters |
| Retweet | **1x** | Baseline amplification |
| Like | **0.5x** | Likes are almost worthless |
| Video watch (50%) | **0.005x** | Video completion matters |

**Negative signals** (these kill your reach):
| Action | Penalty |
|--------|---------|
| Report | **-369x** |
| Block/Mute | **-74x** |

---

## Markov Chain State Graph

This shows how a post moves through states based on engagement:

```
                                    ┌─────────────────────────────────────┐
                                    │                                     │
                                    ▼                                     │
┌─────────────┐    post    ┌─────────────────┐                           │
│             │───────────▶│                 │                           │
│   DRAFTED   │            │  INITIAL PUSH   │                           │
│             │            │  (first 30 min) │                           │
└─────────────┘            └────────┬────────┘                           │
                                    │                                     │
                     ┌──────────────┼──────────────┐                     │
                     │              │              │                      │
                     ▼              ▼              ▼                      │
              ┌───────────┐  ┌───────────┐  ┌───────────┐                │
              │           │  │           │  │           │                │
              │   DEAD    │  │  MODERATE │  │   VIRAL   │                │
              │ (no engmt)│  │  TRACTION │  │  TRACTION │                │
              │           │  │           │  │           │                │
              └───────────┘  └─────┬─────┘  └─────┬─────┘                │
                    │              │              │                       │
                    │              │              │                       │
                    ▼              ▼              ▼                       │
              ┌───────────┐  ┌───────────┐  ┌───────────────┐            │
              │           │  │           │  │               │            │
              │  BURIED   │  │  STEADY   │  │  ALGORITHMIC  │────────────┘
              │           │  │  REACH    │  │  AMPLIFICATION│   (replies
              └───────────┘  └───────────┘  │               │   spark more
                                            └───────────────┘   reach)
```

### State Transitions Explained

**DRAFTED → INITIAL PUSH**
- Your post enters the system
- X shows it to a small test audience (followers + some out-of-network)
- The first 30 minutes are CRITICAL

**INITIAL PUSH → DEAD**
- Transition trigger: No engagement in first 30 min
- Probability: ~70% of posts
- Result: Post gets minimal further distribution

**INITIAL PUSH → MODERATE TRACTION**
- Transition trigger: Some likes, maybe a reply or two
- Probability: ~25% of posts
- Result: Extended reach to more followers

**INITIAL PUSH → VIRAL TRACTION**
- Transition trigger: Multiple replies, especially reply chains
- Probability: ~5% of posts
- Result: Pushed to out-of-network "For You" feeds

**VIRAL TRACTION → ALGORITHMIC AMPLIFICATION**
- Transition trigger: Reply-to-reply chains (75x multiplier)
- This creates a feedback loop — more reach → more replies → more reach
- Posts can re-enter amplification multiple times

---

## The Two Content Sources

X pulls posts from two places:

### 1. Thunder (In-Network)
Posts from people you follow. Stored in real-time memory for instant retrieval.

### 2. Phoenix Retrieval (Out-of-Network)
Posts from people you DON'T follow, discovered by AI based on your interests and engagement history.

Both sources compete for the same feed space, ranked by the same scoring system.

---

## Key Insights

### Replies > Everything
The 75x weight on reply-to-reply is insane. A post that sparks conversation outperforms a post with 100x more likes.

### First 30 Minutes Are Make-or-Break
Early engagement signals "quality" to the algorithm. A post that sits dormant gets buried.

### Negative Signals Are Catastrophic
One block (-74x) wipes out 148 likes (0.5x each). Don't piss people off.

### Likes Are Almost Worthless
At 0.5x weight, likes barely move the needle. They're vanity metrics.

### Video Gets Preferential Treatment
Native video gets 2-4x more reach than text/images. Vertical, 15-60 seconds, with captions.

### External Links Are Punished
Links get 30-50% reach penalty. Workaround: Put links in the first reply.

---

## Premium vs Free Accounts

| Feature | Premium | Free |
|---------|---------|------|
| In-network boost | 4x | 1x |
| Out-of-network boost | 2x | 1x |
| Link penalty | Reduced | Severe |
| Character limit | 25,000 | 280 |

---

## The Tweepcred Score

X assigns each account a credibility score (0-1).

- Below 0.65: Only your 3 best tweets per day get full distribution
- Above 0.65: All tweets eligible for distribution

Factors: Account age, follower/following ratio, engagement history, policy violations.

---

## Sources

- [X Algorithm GitHub Repository](https://github.com/xai-org/x-algorithm)
- [Social Media Today - X Ranking Factors](https://www.socialmediatoday.com/news/x-formerly-twitter-open-source-algorithm-ranking-factors/759702/)
- [Tweet Archivist - Algorithm Breakdown](https://www.tweetarchivist.com/how-twitter-algorithm-works-2025)
- [X Engineering Blog](https://blog.x.com/engineering/en_us/topics/open-source/2023/twitter-recommendation-algorithm)
