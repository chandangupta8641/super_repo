Designing a Scalable Git Strategy for Large Codebases (50GB)
1. Problem Statement
GitHub imposes a 2GB size limit per repository. The requirement is to download and manage code of
approximately 50GB. We must design a strategy that supports cloning, versioning, and check-ins
without violating GitHub limits.
2. Recommended Primary Solution: Multi-Repository Architecture with Git Submodules
This approach divides the 50GB codebase into multiple smaller repositories and links them through a
single “super-repository” using Git submodules.
Why This Works
• Bypasses GitHub’s 2GB limit
• Modular and scalable architecture
• Used in Qualcomm, AOSP, NVIDIA, Google
• Clean branching and independent updates
• Faster CI/CD operations
Folder/Repo Structure Example
super-project/
core/ (submodule)
modules/ (submodule)
assets/ (submodule)
libs/ (submodule)
tests/ (submodule)
Cloning Command
git clone --recurse-submodules <super-repo>
Branching Strategy
• main – stable releases
• develop – integration
• feature/* – new features
• hotfix/* – urgent fixes
• release/* – pre-release staging
3. Secondary Approach: Shallow Clone + Sparse Checkout
Use this to reduce clone size and speed.
Shallow Clone
git clone --depth=1 <repo>
Filtered Clone
git clone --filter=blob:none <repo>
Sparse Checkout
git sparse-checkout init
git sparse-checkout set moduleA moduleB
Use Cases
• Speed up CI builds
• Reduce developer clone time
• Clone only required folders
4. Combined Strategy (Recommended)
• Git Submodules → handle 50GB by modularizing
• Shallow Clone → faster downloads
• Sparse Checkout → selective clone
5. Final Recommendation
Adopt multi-repo architecture with submodules as the primary solution.
Enhance performance using shallow clone and sparse checkout.
This model is scalable, maintainable, and industry■standard for large embedded/firmware systems.


