# Nordorn

A comprehensive personal knowledge management system built in Obsidian, combining Zettelkasten methodology with project management. Uses Templator, Web Clipper, and Zotero integration for automated note creation and academic research management.

## Table of Contents

- [System Overview](#system-overview)
- [Folder Structure](#folder-structure)
- [Core Plugins](#core-plugins)
  - [Templator](#templator)
  - [Web Clipper](#web-clipper)
  - [Zotero Integration](#zotero-integration)
- [Workflow Guides](#workflow-guides)
  - [Project Management](#project-management)
  - [Research & Learning](#research--learning)
  - [Content Curation](#content-curation)
- [Templates](#templates)
- [MOCs (Maps of Content)](#mocs-maps-of-content)
- [Maintenance & Best Practices](#maintenance--best-practices)
- [Setup Instructions](#setup-instructions)

## System Overview

**Nordorn** is a second brain system designed for:
- **Knowledge Management**: Capture, organize, and connect information using Zettelkasten principles
- **Project Tracking**: Manage active projects separately from knowledge areas
- **Academic Research**: Process and synthesize research papers via Zotero integration
- **Learning**: Build interconnected knowledge networks through atomic notes

**Core Philosophy**: Combines the linking power of Zettelkasten with practical project management. Knowledge areas and resources are unified in the Bases system, while projects maintain separate tracking for actionable outcomes.

## Folder Structure

```
~/personal/Nordorn/
├── 00 Bases/           # Core MOCs and system documentation
├── 01 Fleeting Notes/  # Quick captures, temporary thoughts
├── 02 Sources/         # Reference materials, books, articles
├── 03 Tags/            # Tag-based organization and indices
├── 04 Indexes/         # Curated lists and reference guides
├── 05 Base Notes/      # Permanent notes, core concepts
├── 06 Daily Notes/     # Daily journals and planning
├── 07 Projects/        # Active projects and areas
├── 99 Archive/         # Completed or inactive content
├── 99 Templates/       # Note templates for consistency
├── Clippings/          # Web clipper captures
├── Excalidraw/         # Visual diagrams and sketches
└── Images/             # Media assets and attachments
```

### Folder Descriptions

| Folder | Purpose | Content Types |
|--------|---------|---------------|
| **00 Bases** | Knowledge areas and resources | MOCs, topic hubs, areas of responsibility, reference materials |
| **01 Fleeting Notes** | Initial capture | Quick thoughts, meeting notes, temporary ideas |
| **02 Sources** | External references | Book notes, article summaries, Zotero imports |
| **03 Tags** | Topic organization | Tag indices, topic clusters |
| **04 Indexes** | Curated collections | Lists, catalogs, reference materials |
| **05 Base Notes** | Permanent knowledge | Atomic notes, evergreen concepts, linked ideas |
| **06 Daily Notes** | Time-based tracking | Daily journals, planning, reviews |
| **07 Projects** | Active work | Project notes, meeting logs, deliverables |
| **99 Archive** | Inactive content | Completed projects, outdated information |
| **99 Templates** | Note scaffolding | Templator templates for consistency |

## Core Plugins

### Templator

**Purpose**: Automate note creation with dynamic templates

**Key Features**:
- Dynamic date/time insertion
- Automatic folder placement
- Metadata generation
- Custom variable prompts

**Common Templates**:
- Daily Note template with weather, tasks, reflections
- Project kickoff template with objectives and milestones
- Meeting note template with attendees and action items
- Book/Article summary template with key insights
- Fleeting note template with processing workflow

### Web Clipper

**Purpose**: Capture web content directly into Obsidian

**Template Configuration**:
Web clipping template JSON files are stored in `Templates/WebClippings/` folder for consistent formatting and metadata capture.

**Available Clipping Types**:
- **YouTube Videos**: Specialized template for video content with timestamps and key points
- **Default Webpage**: General template for articles, blog posts, and web content

**Workflow**:
1. Clip interesting articles/content to `Clippings/`
2. Process clippings during weekly reviews
3. Extract key insights into `05 Base Notes/`
4. Tag and link to relevant MOCs
5. Archive processed clippings

## Workflow Guides

### Daily Note Workflow

**Morning Routine** (10 minutes):
1. Open today's daily note (auto-created via Templator)
2. Review yesterday's action items
3. Set 3 key priorities for today
4. Check project deadlines and commitments

**Evening Review** (15 minutes):
1. Capture fleeting thoughts from the day
2. Process any new clippings or quick notes
3. Update project progress
4. Plan tomorrow's priorities
5. Reflect on learnings and insights

### Project Management

**Project Initiation**:
1. Create project folder in `07 Projects/`
2. Use project template (objectives, timeline, resources)
3. Create or link to relevant MOC in `00 Bases/`
4. Set up recurring reviews and milestones

**Project Maintenance**:
- Weekly project reviews and updates
- Link related fleeting notes and sources
- Track decisions and lessons learned
- Archive completed projects to `99 Archive/`

### Research & Learning

**Information Processing Pipeline**:
1. **Capture**: Web clipper → `Clippings/`
2. **Initial Processing**: Fleeting note → `01 Fleeting Notes/`
3. **Source Analysis**: Detailed notes → `02 Sources/`
4. **Synthesis**: Permanent note → `05 Base Notes/`
5. **Connection**: Link to relevant MOCs and projects

**Reading Workflow**:
- Use book/article templates for consistent structure
- Extract key quotes and insights
- Create connection notes linking related concepts
- Regular review of source notes for synthesis opportunities

### Content Curation

**Weekly Review Process**:
1. Process all items in `01 Fleeting Notes/`
2. Review and categorize new clippings
3. Update relevant indexes and MOCs
4. Archive completed items
5. Plan next week's learning priorities

## Templates

### Template Categories

**Core Templates**:
- **Daily Note Template**: Daily planning, reflection, and capture
- **Base Note Template**: Atomic knowledge notes following Zettelkasten principles
- **Book Note Template**: Structured book summaries and key insights
- **Zotero Note Template**: Academic paper analysis and citation integration

### Web Clipping Templates

Web clipping template JSON files are stored in `Templates/WebClippings/` folder:
- **YouTube Template**: Video content with timestamps and key points
- **Default Webpage Template**: Articles, blog posts, and general web content

### Template Features

- **Dynamic Variables**: Auto-populated dates, titles, and metadata
- **Conditional Logic**: Templates adapt based on context
- **Prompt Integration**: Interactive fields for custom input
- **Linking Automation**: Auto-generated links to related notes

## MOCs (Maps of Content)

Maps of Content serve as navigation hubs and knowledge dashboards, combining areas of responsibility with resource management.

### Core MOCs in `00 Bases/`

**Knowledge Area MOCs**:
- **Technology MOC**: Programming, tools, and technical concepts
- **Business MOC**: Strategy, management, and professional development
- **Personal MOC**: Health, habits, and personal growth
- **Academic MOC**: Research areas, theories, and scholarly work

**System MOCs**:
- **Home Dashboard**: System overview and quick navigation
- **Project Dashboard**: Active projects and deadlines
- **Learning Dashboard**: Current learning goals and progress

### MOC Structure

```markdown
# MOC Title

## Overview
Brief description and purpose

## Current Focus
Active projects and priorities

## Core Concepts
[[Link]] - Description
[[Link]] - Description

## Recent Updates
- Latest additions and changes

## Related MOCs
Links to connected knowledge areas
```

## Maintenance & Best Practices

### Daily Habits (5-10 minutes)
- Capture thoughts in fleeting notes
- Process urgent clippings
- Update daily note with progress

### Weekly Reviews (30-45 minutes)
- Process all fleeting notes
- Review and categorize clippings
- Update project status
- Clean up tags and links
- Plan next week's priorities

### Monthly Maintenance (1-2 hours)
- Archive completed projects
- Update MOCs with new connections
- Review and refine templates
- Backup and sync vault
- Assess system effectiveness

### Zettelkasten Best Practices

**Atomic Notes**:
- One concept per note
- Self-contained and understandable
- Unique identifiers and clear titles
- Regular linking and cross-referencing

**Linking Strategy**:
- Use `[[double brackets]]` for internal links
- Add context with `[[Note|display text]]`
- Create connection notes for complex relationships
- Build knowledge networks through consistent linking

**Note Development**:
- Start with fleeting notes, develop into permanent notes
- Regular review and refinement of existing notes
- Connect new information to existing knowledge structures
- Maintain note quality over quantity

## ⚙️ Setup Instructions

### Required Plugins
1. **Core Plugins**: Daily notes, Templates, Graph view
2. **Community Plugins**:
   - Templator (advanced templating)
   - Web Clipper (content capture)
   - Zotero Integration (academic research)
   - Dataview (dynamic content)
   - Tag Wrangler (tag management)

### Initial Configuration
1. Set daily notes folder to `06 Daily Notes/`
2. Configure Templator templates folder as `99 Templates/`
3. Set up Web Clipper to save to `Clippings/`
4. Create initial MOCs in `00 Bases/`

### Template Setup
1. Import base templates to `99 Templates/`
2. Configure Templator hotkeys and auto-triggers
3. Test template functionality
4. Customize templates for personal workflow

### First Week Workflow
1. Create your first daily note
2. Set up 2-3 core MOCs
3. Capture and process 5-10 fleeting notes
4. Try the web clipper with interesting articles
5. Review and refine your workflow

---

**Remember**: Your second brain combines the best of Zettelkasten knowledge building with practical project management. Focus on creating atomic, interconnected notes while keeping projects actionable and time-bound.
