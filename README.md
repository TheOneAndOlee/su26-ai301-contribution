# Contribution 2: Hazelnut Bush drops Sweet Berries with Bone Meal  

**Contribution Number:** 2  
**Student:** Osmond Lee  
**Issue:** https://github.com/Let-s-Do-Collection/Let-s-Do-Collection/issues/1054  
**Status:** Phase 2 Complete, but problem was already fixed.

---

## Why I Chose This Issue

Same as before, my goal is to work in the games industry as an engineer/technical designer, and this project is exactly the kind of project I want to work on since it lets me directly work on a gameplay feature. Even more specifically, I've played modded minecraft for years and I've always wanted to contribute to an open source mod. I also already know Java, the language used for this, and it'll serve as a refresher for my Java skills since I haven't used it in a while. From this project, I want to learn more about the minecraft mod development process and have that first bit of experience. That way, I'll feel more confident in contributing to mods in the future and hopefully even make my own mod.

---

## Understanding the Issue

### Problem Description

The hazelnut bush block spawns a sweet when growth is accelerated via bone meal in both survival and creative mode, instead of a hazelnut. Additionally, if fertilizer from `Farm and Charm` (a mod under the same `Let's Do` ecosystem) is used, it correct spawns a hazelnut in survival mode, but fails to spawn anything in creative mode, only making the growth sound.

### Expected Behavior

The hazelnut bush spawns a hazelnut bush if bone meal is used to accelerate growth. Additionally, it should spawn a hazelnut when fertilizer is applied in creative mode.

### Current Behavior

N/A, the code is working, they just never updated their issue list.

### Affected Components

`HazelnutBushBlock.java`

---

## Reproduction Process

### Environment Setup

The only problem encountered during testing was the compilation of the mod, as the `Let's Do` mods require a curseforge and modrinth API key. The best thing to do is make a dummy API key, it will compile fine. Additionally, if there is a delay in downloading independencies, pushing back timeouts is also needed to compile the mod.

### Steps to Reproduce (Windows)

**To reproduce the fixed version**
1. Open the source code for `Let's Do WilderNature` in your IDE of choice.
2. In both the fabric and neoforge folders, go to `Build.gradle` and make a variable named `temp_api_key` and assign it any string value.
3. Scroll down in both `Build.gradle`s to the `curseforge` and `modrinth` tabs and change `apiKey` to your new `temp_api_key` variable.
4. In the root folder's `gradle.properties`, add these arguments to delay any potential timeouts and shut down any reset connections.

`systemProp.http.keepAlive=false  
systemProp.https.keepAlive=false  
systemProp.org.gradle.internal.repository.max.retries=10  
systemProp.org.gradle.internal.repository.max.tentatives=10  
systemProp.org.gradle.internal.repository.initial.backoff=1000`

5. In terminal, run `.\gradlew build`.
6. In the fabric/neoforge folders, go to the build\libs and drag the normal, untagged `letsdo-wildernature-[modpack version]-1.1.5.jar` into your modlauncher of choice, and install `Let's Do Farm & Charm` version 1.1.22 through the mod launcher.
7. In a world, place a hazelnut bush and obtain 5+ bone meal (from normal Minecraft) and fertilizer (from `Let's Do Farm & Charm`).
8. Interact with the hazelnut bush with bone meal and fertilizer. It'll spawn some hazelnuts for both of them.

**To reproduce the original issue**
1. Use any minecraft mod launcher to install `Let's Do Farm & Charm` version 1.1.22 and `Let's do WilderNature` version 1.1.4 to a NeoForge or Fabric instance using Minecraft version 1.21.1.
2. In a world, place a hazelnut bush and obtain 5+ bone meal (from normal Minecraft) and fertilizer (from `Let's Do Farm & Charm`).
3. In survival mode, interact with the hazelnut bush with a bone meal 2 times to grow and harvest the bush. This should spawn a sweet berry instead of a hazelnut.
4. Still in survival mode, interact with the hazelnut bush with fertilizer 2 times to grow and harvest the bush. This should spawn a hazelnut.
5. Finally, switch to creative mode and interact with the hazelnut bush using fertilizer twice. Now, it should spawn nothing.


### Reproduction Evidence
- **Commit showing reproduction:** https://github.com/TheOneAndOlee/WilderNature/tree/fix-issue-1054

**Using the GitHub Repo**
- **Screenshots/logs:** Image 1: Using bone meal correctly spawns a hazelnut: <img width="2557" height="1351" alt="image" src="https://github.com/user-attachments/assets/5b8d349d-efb2-409e-81a0-da6a3f470db4" />


**On the public downloadable platforms (Modrinth/CurseForge)**
- **Screenshots/logs:** Image 1: Using bone meal in survival spawns a sweet berry (incorrect behaviour): <img width="2557" height="1340" alt="image" src="https://github.com/user-attachments/assets/e0f99aea-0382-4273-8213-d333033a0872" />
Image 2: Using fertilizer in survival spawns a hazelnut (correct behaviour): <img width="2557" height="1333" alt="image" src="https://github.com/user-attachments/assets/8c582b12-48bc-4a21-9f9b-288a32db240b" />
Image 3: Using fertilizer in creative mode spawns nothing: <img width="2557" height="1352" alt="image" src="https://github.com/user-attachments/assets/7c11be94-24ab-4107-94c1-ac345cb95fb3" />


- **My findings:** As it turns out, the code was actually fixed. The problem is that the consumer facing source code (on mod installers such as CurseForge & Modrinth are using outdated code. If the code is compiled from source on GitHub, the issue is fixed since they fixed the problem.

---

## Solution Approach

### Analysis

The Hazelnut Bush Block inherits from the `SweetBerryBushBlock` from normal (vanilla) Minecraft. The `SweetBerryBushBlock` comes with 2 methods for interaction: `useItemOn` and `useWithoutItem`. The original code for the hazelnut bush had a case where if bone meal was used on an non-fully grown hazelnut bush, it would go to the default interaction, which was hardcoded to return a sweet berry.

### Proposed Solution

N/A, the code is already fixed.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** [Restate the problem]

**Match:** [What similar patterns/solutions exist in the codebase?]

**Plan:** [Step-by-step implementation plan]
1. [Modify file X to do Y]
2. [Add function Z]
3. [Update tests]

**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** [How will you verify it works?]

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

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
