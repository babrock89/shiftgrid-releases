# ShiftGrid User Manual

**Version 0.1.0**

---

## Table of Contents

1. [Introduction](#introduction)
2. [Getting Started](#getting-started)
3. [Navigation](#navigation)
4. [Asset Configuration](#asset-configuration)
5. [Roster Management](#roster-management)
6. [Team Member Availability](#team-member-availability)
7. [Teams Management](#teams-management)
8. [Creating Shift Demands](#creating-shift-demands)
9. [Shift Backlog](#shift-backlog)
10. [Schedule Management](#schedule-management)
11. [Monthly Calendar View](#monthly-calendar-view)
12. [Analytics](#analytics)
13. [Project Management](#project-management)
14. [Importing and Exporting Data](#importing-and-exporting-data)
15. [Help Menu](#help-menu)
16. [Tips and Best Practices](#tips-and-best-practices)

---

## Introduction

ShiftGrid is a desktop application for managing shift assignments across multiple assets and teams. It provides:

- Flexible asset and shift configuration
- Team and roster management with POC (Point of Contact) tracking
- Team member availability calendars with import support
- Demand-based shift generation with optional POC assignment
- Drag-and-drop schedule management
- Auto-scheduling with intelligent conflict detection
- Analytics dashboard with schedule health metrics
- Monthly calendar view for at-a-glance schedule overview
- CSV import and export for data portability

---

## Getting Started

### First Launch

When you first launch ShiftGrid, a **Project Manager** dialog appears with options to:

- **Create New Project** - Start fresh with a new project
- **Open Existing Project** - Load a previously saved project
- **Recent Projects** - Quick access to recently opened projects
- **Start Without Project** - Use defaults without saving to a project folder

### Recommended Workflow

1. Configure your **Assets** (locations, operating hours, shifts)
2. Add team members to the **Roster**
3. Create **Teams** and assign roster members
4. Define **Shift Demands** (which teams need shifts, in which assets)
5. Generate shifts to the **Backlog**
6. Use **Auto Schedule** or drag-and-drop to populate the **Schedule**
7. **Export** the final schedule to CSV

---

## Navigation

The application has a left sidebar with seven main pages:

| Page | Description |
|------|-------------|
| **Assets** | Configure assets, operating hours, and shift lengths |
| **Roster** | Manage all team members (POCs) in one place |
| **Teams** | Create teams and assign roster members |
| **Create Demand** | Define how many shifts each team needs |
| **Shift Backlog** | View generated shifts waiting to be scheduled |
| **Schedule** | The main calendar grid for placing shifts |
| **Analytics** | Schedule health metrics, utilization, and workload analysis |

The sidebar also shows:
- Current project name (click to open Project Manager)
- **Save** button - Save current project
- **Save As** button - Save to a new location
- Backlog count indicator

---

## Asset Configuration

### Adding an Asset

1. Navigate to the **Assets** page
2. Click **Add Asset**
3. Configure the asset settings:

### Asset Settings

| Setting | Description |
|---------|-------------|
| **Name** | Display name for the asset |
| **Start Hour** | When the asset opens (e.g., 6:00 AM) |
| **End Hour** | When the asset closes (e.g., 22:00 / 10 PM) |
| **Days of Operation** | Which days the asset is open (checkboxes for Sun-Sat) |
| **Half Days** | Mark specific days as half days with custom end times |
| **Capabilities** | Special features/equipment available at this asset |

### Configuring Shifts

Each asset can have multiple shift types per day:

1. Click **Add Shift** within an asset card
2. Set the **shift length** in hours (e.g., 8 hours)
3. Add more shifts if needed (e.g., two 8-hour shifts = 16 hours coverage)

The system calculates total configured hours vs. available hours automatically.

### Asset Capabilities

Capabilities are managed at the project level in a collapsible section above the assets grid. They represent special features or resources (e.g., "High Security", "Equipment X"):

1. Expand the **Capabilities** section on the Assets page
2. Type a capability name and click **Add**
3. For each capability, you can:
   - **Rename** — Click the capability name to edit it inline
   - **Toggle Shared Resource** — Mark the capability as a limited shared resource
   - **Set Available Quantity** — When shared, specify how many can be used concurrently across all assets
   - **Assign to Assets** — Use toggle buttons to assign/unassign the capability to specific assets

On individual asset cards, capabilities appear as toggle buttons (no free-form input — select from the project-level list).

#### Shared Resource Constraints

When a capability is marked as a shared resource with a quantity limit:
- **Drag-and-drop**: A warning appears if scheduling a shift would exceed the shared resource's available quantity in that time slot across all assets
- **Auto-scheduler**: Treats the shared resource capacity as a hard constraint and will not exceed it

---

## Roster Management

The Roster page is a centralized list of all team members (POCs) before assigning them to teams.

### Adding Team Members

**Manually:**
1. Enter **First Name** and **Last Name**
2. Optionally enter a **Username** (e.g., network login, tool username)
3. Press Enter or click **Add**

**Bulk Import:**
1. Click **Import CSV**
2. Select a CSV file (.csv)
3. The system auto-detects name columns:
   - Columns with "First" and "Last" in headers
   - Or a single "Name" column with "First Last" or "Last, First" format
4. An optional "Username" column (also matches "User Name" or "User") is imported if present
5. Duplicates are automatically skipped

### Assigning to Teams

1. Click the team selector dropdown next to a roster member
2. Check/uncheck teams to assign or remove the member
3. Assigned teams appear as colored badges on the member's row

### Removing Members

Click the **X** button next to a member to remove them from the roster. This also removes them from all teams they were assigned to.

---

## Team Member Availability

Each team member can have unavailable dates marked on their calendar. This affects scheduling warnings and auto-scheduler decisions.

### Viewing Availability

On the **Roster** page, each team member has a **calendar icon** button:
- The icon shows a **badge** with the count of unavailable dates (if any)
- Click the icon to expand/collapse the availability editor

### Manually Editing Unavailable Dates

When the availability section is expanded:

1. **View existing dates** - Unavailable dates are displayed as chips, sorted chronologically (e.g., "Feb 3, 2026")
2. **Add a new date** - Use the date picker and click **Add**
3. **Remove a date** - Click the **X** button on any date chip
4. Duplicate dates are prevented automatically

### Importing Availability from File

For bulk updates, import unavailable dates from CSV or Excel files:

1. Click **Import Availability** on the Roster page
2. **Upload** a CSV or Excel file (.csv, .xlsx, .xls)

#### Supported File Formats

**Calendar Matrix (Recommended):**
Names in the first column, dates as column headers. Any value in a cell means unavailable, blank means available.

| Name | Feb 3 | Feb 4 | Feb 5 |
|------|-------|-------|-------|
| Smith, John | | PTO | |
| Jane Doe | X | | X |

**Name + Dates Column:**
Each row has a name and semicolon-separated dates.

| Name | Unavailable Dates |
|------|-------------------|
| John Smith | 2026-02-03; 2026-02-05 |

**Date Range Format:**
Each row has a name with start and end dates (auto-expanded to individual dates).

| Name | Start Date | End Date |
|------|------------|----------|
| John Smith | Feb 3, 2026 | Feb 7, 2026 |

**Single POC Format:**
Dates only (no names). You select the team member from a dropdown.

| Unavailable Date |
|------------------|
| 2026-02-03 |
| 2026-02-05 |

#### Name Format Flexibility

Names can be in any of these formats (even mixed in the same file):
- "First Last" (e.g., John Smith)
- "Last, First" (e.g., Smith, John)
- Separate "First Name" and "Last Name" columns

#### Date Format Flexibility

Dates are auto-detected and can be:
- ISO: 2026-02-03
- US: 02/03/2026
- European: 03/02/2026
- Natural: Feb 3, 2026 or February 3rd, 2026

#### Import Modes

- **Merge** - Add imported dates to existing unavailable dates
- **Replace** - Clear existing dates and use only imported dates

#### Import Wizard Steps

1. **Upload** - Drag and drop or browse for file
2. **Configure** - Select POC (for single-POC format) or confirm detected format
3. **Preview** - Review matched entries and warnings for unmatched names
4. **Confirm** - Choose merge vs. replace mode and complete import

### How Availability Affects Scheduling

**Drag-and-Drop Warnings:**
- When scheduling a shift, the system checks POC availability
- If team members are unavailable (by calendar or other shift conflicts), a warning appears
- Warns if fewer than the minimum required POCs would be available

**Auto-Scheduler:**
- Treats unavailable dates as hard constraints
- Will not place shifts when insufficient POCs are available
- Respects both calendar unavailability and shift overlap conflicts

---

## Teams Management

### Creating a Team

1. Navigate to the **Teams** page
2. Click **Add Team**
3. Configure:
   - **Team Name** - Display name
   - **Color** - Click the color swatch to choose a color for visual identification

### Assigning POCs to Teams

When the roster has members:
1. Click the POC selector dropdown
2. Search/filter by typing
3. Check members to add, uncheck to remove
4. Use "Select All" or "Clear All" for quick actions

### Minimum Required POCs

Each team has a **Minimum required POCs for shifts** setting:

- Determines how many team members must be available for a shift
- Default: 0 POCs = 0 required, 1 POC = 1 required, 2+ POCs = 2 required
- Adjust manually from 0 to the team's total POC count
- When set to 0, POC availability checks are skipped

This affects:
- Warnings when scheduling (if not enough POCs are available)
- Auto-scheduler decisions (won't place shifts with POC conflicts)

---

## Creating Shift Demands

Demands define how many shifts each team needs and where they can be placed.

### Adding a Demand

1. Navigate to **Create Demand**
2. Click **Add Demand**
3. Configure:

| Field | Description |
|-------|-------------|
| **Team** | Which team needs these shifts |
| **Demand Type** | Fixed Quantity or Recurring Pattern (see below) |
| **Quantity / Pattern** | Number of shifts or recurrence pattern |
| **Priority** | 1-10, higher priority = scheduled first (default: 5) |
| **Min Required POCs** | Override the team default for this demand |
| **Required Capabilities** | Assets must have these capabilities |
| **Compatible Assets** | Which assets can these shifts be placed in |
| **Assign Members** | Optional toggle to assign specific POCs to individual shifts |
| **Note** | Optional text that appears on shift cards |

### Demand Modes

Each demand can operate in one of two modes:

**Fixed Quantity:**
- Specify the exact number of shifts needed
- Works the same as a simple quantity entry
- Shifts remain static regardless of schedule date changes

**Recurring Pattern:**
- Specify a pattern instead of a fixed number
- The quantity is automatically calculated from the schedule period
- Updates automatically when schedule dates change
- Available pattern types:
  - **Every Weekday** - One shift for each Monday through Friday
  - **N per Week** - A set number per week (1-5)
  - **Specific Day** - A particular day of the week, with optional week-of-month filter (Every, First, Second, Third, Fourth, Last)
- The calculated quantity appears in a blue box showing the date range
- A warning appears if the pattern produces 0 shifts for the current date range

**Examples:**
- "Every Weekday" over a 2-week span = 10 shifts
- "3x per Week" over 14 days = 6 shifts
- "Every Monday" over 3 weeks = 3 shifts
- "First Monday" over Feb-Mar = 2 shifts

### Dynamic Backlog Sync (Recurring Demands)

When using recurring patterns, the backlog automatically stays in sync with your schedule dates:

- **Extending the schedule** adds new shifts to the backlog
- **Shortening the schedule** removes excess backlog shifts
- Already-scheduled shifts are never affected — only backlog shifts are adjusted
- Deleting a recurring demand also removes its associated backlog shifts

### Required Capabilities

1. Select capabilities the shift requires
2. Assets without those capabilities are automatically disabled (greyed out)
3. Disabled assets show a tooltip explaining which capabilities are missing

### POC Assignment to Shifts

When the **Assign Members** option is enabled on a demand:

**During Drag-and-Drop:**
- When you drop a shift onto the schedule, a **POC Assignment Modal** appears
- Available POCs are shown as selectable checkboxes; unavailable POCs are greyed out with a reason (shift conflict, calendar unavailability, etc.)
- You must select at least the minimum required number of POCs before confirming
- Cancelling the modal cancels the drop entirely

**During Auto-Scheduling:**
- POCs are automatically assigned based on availability
- The algorithm distributes shifts fairly — POCs with fewer total shifts are preferred
- Distribution is tracked globally across all teams for shared POCs

**Display:**
- Shift cards show "(N)" after the team name indicating the number of assigned POCs
- Schedule grid slots show "N assigned" text below the asset name
- Hover tooltips show the full list of assigned POC names

### Shift Detail Modal

Click any shift card (in the backlog or on the schedule) to open a detailed view showing:
- Date, time, and duration
- Team info with full roster and assigned POC highlighting
- Compatible assets
- Required capabilities with match indicators
- Recurrence pattern (if applicable)
- Notes

Click outside the modal or press the Close button to dismiss.

### Generating Shifts

1. Configure all your demands
2. Click **Create Shifts**
3. Shifts are generated to the Backlog based on demand quantities

---

## Shift Backlog

The Backlog shows all generated shifts waiting to be scheduled.

### Summary Statistics

- **Total Shifts** - All shifts created from demands
- **Assigned** - Shifts placed on the schedule
- **In Backlog** - Shifts waiting to be scheduled
- **Progress Bar** - Visual completion percentage

### Shift Breakdown Table

Shows shifts grouped by demand with:
- Team name and color
- Compatible assets
- Priority level
- Scheduled vs. backlog counts
- Required capabilities
- Notes (hover to see full text)

### Managing the Backlog

- **Clear All Backlog** - Remove all unscheduled shifts (with confirmation)
- **Clear Row (X)** - Remove unscheduled shifts for a specific demand group

---

## Schedule Management

### Schedule Period

Set the date range at the top of the Schedule page:
- **From** date - Start of the schedule
- **To** date - End of the schedule
- Days count is calculated automatically

### The Schedule Grid

The grid shows:
- **Rows** = Assets
- **Columns** = Days (with date and day of week)
- **Cells** = Available shift slots

Each cell displays:
- Filled shifts (colored by team)
- Empty slots (dotted outline showing shift length)
- Hours used / max hours and utilization percentage

### Drag and Drop

**From Backlog to Schedule:**
1. Drag a shift from the backlog sidebar
2. Drop on an empty slot in a compatible asset
3. Incompatible assets are greyed out while dragging

**Moving Shifts:**
- Drag between days/assets
- Drag to a specific slot within a day
- Drag back to backlog to unschedule

### Auto Schedule

Click **Auto Schedule** to automatically place all backlog shifts.

#### Auto-Scheduler Settings

Click the **gear icon** next to "Auto Schedule" to open the settings popover:

| Setting | Range | Default | Description |
|---------|-------|---------|-------------|
| **Mode** | Spread / Compress | Spread | How shifts are distributed (see below) |
| **Max consecutive days** | 1-14 | 3 | Maximum days a team can work in a row |
| **Max shifts per team/day** | 1-5 | 1 | Maximum shifts one team can have per day |

All settings are saved with your project.

**Spread Mode (default):**
- Spreads shifts evenly across the schedule period
- Prefers early shifts (slot 0) for all teams
- Only uses late shifts when necessary
- Balances late shifts fairly across teams
- Respects recurring demand patterns (prefers matching days)

**Compress Mode:**
- Packs shifts into the shortest time possible
- Fills all slots on a day before moving to the next
- Ignores recurrence patterns (maximizes density)

**Constraints respected (both modes):**
- Asset compatibility and capabilities
- Days of operation (closed days)
- Maximum shifts per team per day
- Maximum consecutive days
- Late-to-early shift rules (no early shift after a late shift)
- POC availability conflicts

#### Auto-Scheduler Diagnostics

After auto-scheduling, if any shifts could not be placed, a **diagnostics modal** automatically appears showing:

1. **Summary** — Total, Placed (green), and Failed (red) counts with a progress bar
2. **Failure Breakdown** — Bar chart showing why shifts were rejected (e.g., "Consecutive days limit", "Slot already filled", "POC unavailable")
3. **Per-Team Details** — Expandable sections for each team showing their specific rejection reasons and sample messages
4. **Configuration Used** — The settings that were active during the run

After closing the modal, a **Results** button appears on the Schedule header. Click it anytime to re-view the diagnostics from the last run.

### Warnings

The system warns you about:
- **Same-day conflicts** - Team scheduled in multiple assets on the same day
- **Late-to-early conflicts** - Early shift the day after a late shift
- **POC conflicts** - Not enough available team members due to overlapping shifts

Warnings appear as modal dialogs that must be acknowledged.

### Clear Schedule

Click **Clear** to move all scheduled shifts back to the backlog (with confirmation).

---

## Monthly Calendar View

The Schedule page includes a **Calendar** tab that provides a traditional month-at-a-glance view of the schedule for a selected asset.

### Viewing the Calendar

1. Navigate to the **Schedule** page
2. Click the **Calendar** tab (next to the grid view)
3. Select an asset from the **Asset** dropdown

### Calendar Features

- **Sun–Sat grid** — Traditional 7-column weekly layout showing one month at a time
- **Color-coded shift blocks** — Each shift displays as a colored block using the team's color, showing the team name and time range (e.g., "06:00–14:00")
- **Month navigation** — Use the prev/next arrows to move between months. Navigation is constrained to months that overlap with the schedule period
- **Today highlighting** — Today's date is highlighted with a blue circle. The calendar auto-scrolls to the current month on load
- **Hover tooltips** — Hover over a shift block to see full details including assigned POCs and notes
- **Day states** — Days outside the schedule period are grayed out. Days when the asset is closed show a "Closed" label

### Printing

Click the **Print** button to generate a print-friendly layout with the asset name, month, date range, and generation timestamp in the header.

---

## Analytics

The **Analytics** page provides a read-only dashboard of schedule health and metrics. It updates live as the schedule changes.

### Schedule Summary

Card grid showing key metrics:
- **Total scheduled shifts** and **backlog shifts**
- **Active assets** and **active teams**
- Completion progress bar
- Schedule period display

### Demand Fulfillment

Per-demand breakdown showing how many shifts have been scheduled vs. the total required:
- Progress bars for each demand
- Status badges: **Complete** (green), **Partial** (amber), **Unscheduled** (gray)
- Summary counts at the bottom

### Asset Utilization

Per-asset horizontal bar charts showing the percentage of available slots filled:
- Respects days of operation and half-day configurations
- Color-coded bars (green for high utilization, amber for low)

### Team Shift Analysis

Per-team breakdown showing:
- Total shift count
- Early vs. late shift counts (as badges)
- Distribution across assets

### Team Member Workload

Shown only when POC assignment data exists in the schedule:
- Table with per-POC shift counts
- Early/late breakdown and team/asset distribution
- Highlights workload imbalances (>50% deviation from team mean) with amber warnings

### Printing

Click the **Print** button to generate a print-friendly report. The sidebar and non-essential UI are hidden, and page breaks are placed to keep sections together.

---

## Project Management

### Project Structure

Each project is stored in a folder containing:
- `config.json` - Assets, teams, roster, schedule period
- `schedule.json` - Demands, backlog, and scheduled shifts
- `outputs/` - Exported CSV files

### Saving

- **Save** (sidebar) - Save to current project location
- **Save As** (sidebar) - Save to a new location with a new name

### Unsaved Changes

When you close the application with unsaved changes, a prompt appears with four options:

- **Save Project** — Save to the current project location and close (disabled if no project is open)
- **Save as New Project** — Opens the Save As flow to save to a new location, then closes
- **Cancel** — Stay in the application
- **Exit Without Saving** — Close immediately without saving

If no changes have been made since the last save, the app closes immediately without prompting.

### Loading

From the Project Manager:
- **Full Load** - Restores everything (config + schedule)
- **Config Only** - Imports asset setup without schedule data (useful for reusing configurations)

---

## Importing and Exporting Data

### CSV Export

1. Navigate to the **Schedule** page
2. Click **Export**
3. If a project is open, the file saves to `outputs/` folder
4. Otherwise, it downloads directly

#### Export CSV Columns

| Column | Description |
|--------|-------------|
| Team Name | Name of the assigned team |
| Team Members | Semicolon-separated list of team POCs (assigned POCs only if POC assignment is enabled) |
| Usernames | Semicolon-separated usernames from roster (if set) |
| Asset | Asset name where shift is scheduled |
| Start Date/Time | Shift start (e.g., "2026-01-27 06:00") |
| End Date/Time | Shift end (e.g., "2026-01-27 14:00") |
| Notes | Required capabilities and user-entered notes |

---

### Schedule Import

Import an existing schedule from CSV or Excel files to populate the schedule grid.

#### Starting an Import

1. Navigate to the **Schedule** page
2. Click **Import**
3. Drag and drop or browse for a CSV/Excel file

#### Required Columns

Your import file must have these columns:
- **Lab** - Name of the lab (must match an existing lab)
- **Start Date/Time** - When the shift starts (e.g., "2026-01-27 06:00")
- **End Date/Time** - When the shift ends (e.g., "2026-01-27 14:00")

#### Optional Columns

- **Team Name** - If missing or unmatched, shift shows as "Unavailable" in grey
- **Team Members** - Preserved for reference but not validated
- **Notes** - Any notes attached to the shift

#### Supported Date/Time Formats

- "YYYY-MM-DD HH:MM" (e.g., "2026-01-27 06:00")
- "MM/DD/YYYY HH:MM" (e.g., "01/27/2026 06:00")

#### Asset and Team Matching

- **Assets** - Matched case-insensitively against existing assets
  - Unmatched assets result in errors (shifts skipped)
- **Teams** - Matched case-insensitively against existing teams
  - Unmatched or empty team names show as **"Unavailable"** with grey color

#### Import Modes

**Replace Mode:**
- Clears the existing schedule completely
- Uses only the imported shifts

**Merge Mode:**
- Adds imported shifts alongside existing scheduled shifts
- When conflicts occur (same day/lab/slot), shows a **conflict resolution** dialog

#### Conflict Resolution

When merging and conflicts are detected:

1. A modal shows all conflicting shifts
2. For each conflict, you see side-by-side:
   - **Current** - The existing shift already on the schedule
   - **Imported** - The shift from your import file
3. Click to select which version to keep for each conflict
4. Use quick actions: **"Keep all existing"** or **"Use all imported"**
5. Click **Apply Changes** to complete the merge

**What happens to resolved shifts:**
- **Keep existing** - The imported shift is discarded
- **Use imported** - The existing shift is moved back to the backlog

#### Import Wizard Steps

1. **Upload** - Select your CSV or Excel file
2. **Preview** - Review matched shifts, warnings, and errors
   - See which labs and teams were matched
   - See counts of shifts to import
   - Review any parse errors (skipped rows)
3. **Confirm** - Choose merge vs. replace mode and import

#### Example Import File

```csv
"Team Name","Lab","Start Date/Time","End Date/Time","Notes"
"Team Alpha","Lab A","2026-01-27 06:00","2026-01-27 14:00","Morning shift"
"Team Beta","Lab A","2026-01-27 14:00","2026-01-27 22:00","Evening shift"
"Team Alpha","Lab B","2026-01-28 06:00","2026-01-28 14:00",""
```

#### Tips for Successful Imports

- **Lab names must match exactly** (case-insensitive) - "Lab A" matches "lab a"
- **Shifts must fit existing lab slots** - Start times and durations must match configured shifts
- **Dates must be within schedule period** - Shifts before the start date are rejected
- **Use the exported format** - Export a schedule first to see the exact format expected

---

## Help Menu

ShiftGrid includes a built-in user manual accessible from the application menu bar.

### Accessing the Manual

1. Click **Help** in the menu bar at the top of the application window
2. Click **User Manual**
3. The manual opens in a new window with formatted content

The Help menu is available at all times while the application is running. The manual window can be kept open alongside the main application for reference.

---

## Tips and Best Practices

### Planning Your Schedule

1. **Start with assets** - Configure all locations before adding teams
2. **Build your roster first** - Add all personnel before creating teams
3. **Use capabilities** - Tag assets with special features to ensure proper shift placement
4. **Set realistic minimums** - Configure minimum POCs to catch availability issues early

### Efficient Scheduling

1. **Use Auto Schedule first** - Let the algorithm do the heavy lifting
2. **Fine-tune with drag-and-drop** - Adjust individual shifts as needed
3. **Watch for warnings** - They highlight potential issues
4. **Check the backlog** - Ensure all shifts got scheduled

### Managing Team Member Availability

1. **Import availability early** - Load PTO/vacation calendars before creating demands
2. **Use calendar matrix format** - Easiest to create and import from spreadsheets
3. **Merge vs. Replace** - Use merge to add new dates, replace to sync with an external calendar
4. **Check badge counts** - The calendar icon badge shows how many unavailable dates each person has

### Importing Schedules

1. **Export first** - Export a sample schedule to see the exact format expected
2. **Match asset names exactly** - Asset names must match your configured assets (case-insensitive)
3. **Use merge for updates** - Import changes and resolve conflicts individually
4. **Check for errors** - Review the preview step for any skipped rows
5. **Unknown teams become "Unavailable"** - Useful for blocking time slots without a specific team

### Avoiding Common Issues

- **Greyed-out assets while dragging?** - The shift's compatible assets don't include that asset
- **Can't place shift?** - All slots may be filled, or it violates a constraint
- **POC warnings?** - Team members are already scheduled elsewhere at that time
- **Auto-schedule didn't place all shifts?** - Check backlog; some may be unplaceable due to constraints
- **Import errors?** - Asset names must match exactly; dates must be within schedule period
- **Import conflicts?** - Use the conflict resolution dialog to choose which shifts to keep

### Keyboard Shortcuts

- **Enter** in text fields - Submit/add the item
- **Escape** - Close modals and dropdowns

---

## Support

For issues or feature requests, visit:
https://github.com/babrock89/shiftgrid-app/issues

---

*ShiftGrid v0.1.0 - Built with React and Electron*
