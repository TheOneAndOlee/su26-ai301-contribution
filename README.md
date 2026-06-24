# Contribution 2: [Furniture] Display still displays item after it's been removed

**Contribution Number:** 2
**Student:** Osmond Lee  
**Issue:** https://github.com/Let-s-Do-Collection/Let-s-Do-Collection/issues/1036  
**Status:** Phase 3 Complete

---

## Why I Chose This Issue

My goal is to work in the games industry as an engineer/technical designer, and this project is exactly the kind of project I want to work on since it lets me directly work on a gameplay feature. Even more specifically, I've played modded minecraft for years and I've always wanted to contribute to an open source mod. I also already know Java, the language used for this, and it'll serve as a refresher for my Java skills since I haven't used it in a while. From this project, I want to learn more about the minecraft mod development process and have that first bit of experience. That way, I'll feel more confident in contributing to mods in the future and hopefully even make my own mod.

---

## Understanding the Issue

### Problem Description

When you retrieve an item in a display case, you successfully recieve the item but the item is still visually in the display case.

### Expected Behavior

The item should no longer be visible inside of the display case.

### Current Behavior

The item is visible inside of the display case after retrieval

### Affected Components

The java files containing the display block logic. This includes:
1. `DisplayBlock.java`
2. `DisplayBlockEntity.java`
3. `DisplayRenderer.java`

---

## Reproduction Process

### Environment Setup

To make the installation process easier, I recommend using Modrinth, CurseForge, or any other established mod/modpack installer.

### Steps to Reproduce

1. Use any minecraft mod launcher to install *Let's Do Furniture* version 1.1.4 to a NeoForge or Fabric instance using Minecraft version 1.21.1.
2. In a world, place a display case and any item into it.
3. Interact with the display case again with an empty hand to retrieve your item.
4. You have your item in your hand, but the display case visually also has the item.

### Reproduction Evidence

- **Commit showing reproduction:** N/A - Reproduction can be done in through public mod installation. Compilation of the repo directly is not necessary.
- **Screenshots/logs:** An image of the display case actively holding the enchanted golden apple. <img width="2557" height="1350" alt="image" src="https://github.com/user-attachments/assets/df198387-d916-4afe-bef3-e335a96c1742" />

After retrieval of the item. The enchanted golden apple is currently in my hand and the apple is not retrievable inside the display case. This is because the apple has been removed on the server-side, but not visually on the client side.
<img width="2557" height="1350" alt="image" src="https://github.com/user-attachments/assets/683e81e1-2ab0-4382-8831-cf77db2e58a5" />

- **My findings:** Bug is exactly as the issue described on the stated version.
---

## Solution Approach

### Analysis

The logic that handles item visibility in the display case successfully removes the item on the server, but the clients are returned nothing, so the clients don't visually update the display case.

### Proposed Solution

The plan is to return a successful item retrieval, so the clients will update the visuals.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** The display case block visually contains an item even after it has been removed. It should no longer be visible in the display case.

**Match:** The Wardrobe and Bin blocks have this pattern, but have a safer pattern. They use an early client check to ensure that all clients update.

**Plan:** 
1. Modify `DisplayBlock.java` to use the same early return pattern as the Wardrobe and Bin blocks.
2. Compile, install, and test to ensure functionality.

**Implement:** My branch: https://github.com/TheOneAndOlee/Let-s-Do-Furniture-Fork

**Review:** Items as suggested from `Contributing.md`:
- [x] Maintain consistent code style
- [x] Keep code clean and organized
- [x] Avoid leaving unused code
- [x] Keep commit messages clear and concise

**Evaluate:** Compile the mod and add it to a modded minecraft instance to test the fix.

---

## Testing Strategy

### Unit Tests

- [ ] Test case: Build, add it to a modpack, and test it in Minecraft.

### Integration Tests

- N/A, there's no code tests

### Manual Testing

It works now! The object properly disappears when retrieved.

---

## Implementation Notes

### Week 3 Progress

I built the file for both fabric and neoforge, struggled a little bit with some unsuccessful fixes, but after using Claude and figuring out how the call stack works, I was able to implement and test a working fix.

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** `DisplayBlockEntity.java`
- **Key commits:** [Link](https://github.com/Let-s-Do-Collection/Furniture/commit/fa66cb16c1459026eaf3f8734c30fd93c4a53fbd)
- **Approach decisions:** I immediately looked at the original DisplayBlock.java, but my fixes didn't work, and after more learning via Claude, realized that my changes wouldn't affect the client-side, so I learned about the call stack. After learning about the call stack, I looked through DisplayBlockEntity.java since I saw that similar blocks such as the Wardrobe didn't have the same issue, meaning the DisplayRenderer most likely wasn't the problem. 

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
