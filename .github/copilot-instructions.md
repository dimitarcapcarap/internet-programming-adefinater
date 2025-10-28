# Instructions for Generating Internet Programming Exam Materials

## Context
Generate materials for a 2-hour practical exam for 70 students testing JavaScript/TypeScript web development skills. Students will use LLMs and online resources. The exam should be easy to pass (60%) but hard to excel (90%+), creating natural grade variance.

## Files to Generate

### 1. Exam Specification (`exam-specification.md`)

Create a complete exam specification based on the Doctor Who episode viewer assignment with these modifications:

**Tier 1 Requirements (60 points - Basic Functionality):**
- Display episodes in a table with: rank, title, series, era, broadcast year, director, writer, doctor (actor + incarnation), companion (actor + character), cast count
- Single-column sorting (ascending/descending toggle)
- Name filter (text input, case-insensitive contains)
- Fetch data from provided JSON file
- Display loading state

**Tier 2 Requirements (25 points - Edge Case Handling):**
- Handle missing/null companions gracefully (display "None" or "—")
- Handle episodes with empty cast arrays
- Handle multiple writers in a single string (e.g., "Writer A & Writer B")
- Sort dates correctly even with mixed formats in data
- Handle special characters in titles (quotes, apostrophes, hyphens)
- Display error message if data fetch fails

**Tier 3 Requirements (15 points - Advanced Features):**
Students choose 2 of these 4 options (5 points each, can earn up to 15 total):

1. **Performance Optimization**: Page must remain responsive with 1000+ episodes. Include comment explaining optimization strategy (virtualization, debouncing, etc.)

2. **Keyboard Navigation**: Arrow keys navigate table, Enter key sorts by current column, Tab/Shift+Tab move between filters

3. **Smart Relevance Sort**: When search filter is active, sort by:
   - Exact title match first
   - Title contains search term second  
   - Any field contains search term third
   - Then by rank

4. **Data Validation**: Console warnings for suspicious data (missing required fields, future dates, duplicate ranks, negative series numbers). Display warning count in UI.

**Bonus Tasks (5 points each, optional):**
- Multi-column sorting (shift+click)
- Era filter dropdown
- Doctor filter dropdown (populated from data)
- Companion filter dropdown (populated from data)
- Export filtered results to CSV
- Decade grouping display

**Personalization:** Generate 5 variants with different Tier 2 combinations. Each variant should have same total points available but different specific requirements.

### 2. Test Data File (`doctor-who-episodes-exam.json`)

Generate a JSON file with ~150 episodes that includes these INTENTIONAL edge cases:

**Edge Cases to Include (distribute throughout data):**
- 10% of episodes with `"companion": null`
- 5% with empty cast arrays `"cast": []`
- 15% with multiple writers: `"writer": "Name1 & Name2"` or `"writer": "Name1 and Name2"`
- Mixed date formats:
  - 60%: `"broadcast_date": "YYYY-MM-DD"` (ISO format)
  - 20%: `"broadcast_date": "DD/MM/YYYY"`
  - 15%: `"broadcast_date": "Month DD, YYYY"`
  - 5%: `"broadcast_date": "YYYY"` (year only)
- Special characters in titles:
  - Apostrophes: `"The Doctor's Wife"`
  - Quotes: `"The \"Deadly\" Assassin"`
  - Hyphens: `"Doctor Who - The Movie"`
  - Slashes: `"Bad Wolf / The Parting of the Ways"`
  - Parentheses: `"Time (Part 1)"`
- Some doctors/companions with accented characters: `"Señor Doctor"`
- Include 2-3 suspicious/invalid entries:
  - One with future broadcast date
  - One with negative rank
  - One with rank = 0
  - One with missing required field (e.g., no title)

**Data Distribution:**
- Classic era: 40 episodes (1963-1989)
- Modern era: 70 episodes (2005-2017)  
- Recent era: 40 episodes (2018-2025)
- Ensure variety of doctors, companions, directors, writers
- Ranks should be 1-150 with 2-3 duplicates or gaps to test validation

### 3. Grading Rubric (`grading-rubric.md`)

Create a detailed rubric with:

**Tier 1 (60 points):**
- Data loads and displays: 15 points
- Table rendering: 10 points
- Single-column sort: 15 points
- Name filter: 10 points
- Loading state: 5 points
- Basic error handling: 5 points

**Tier 2 (25 points):**
- Null companion handling: 5 points
- Empty cast handling: 3 points
- Multiple writers display: 3 points
- Date sorting with mixed formats: 7 points
- Special characters rendering: 4 points
- Error message display: 3 points

**Tier 3 (15 points):**
- Each advanced feature: 5 points (choose 2)
- Partial credit for attempted but incomplete features
- Must document optimization approach

**Bonus (25 points max):**
- Each bonus feature: 5 points

**Deductions:**
- Console errors on load: -5 points
- Page crashes on any interaction: -10 points
- Code doesn't run without modification: -15 points

### 4. Automated Test Suite (`test-suite.html`)

Create an HTML file with embedded JavaScript that:

**Functionality:**
- Takes a URL/path to student submission
- Loads it in an iframe
- Programmatically tests basic functionality:
  - Data loads (check table has rows)
  - Sort buttons exist and work
  - Filter input exists
  - Edge case data renders without errors
- Generates a preliminary score report
- Outputs JSON with test results

**Tests to Include:**
```javascript
// Basic tests
- Page loads without errors
- Table contains >100 rows
- Each row has correct number of columns
- Sort buttons/headers exist
- Filter input exists
- Filter triggers on input

// Edge case tests  
- Null companion doesn't show "null" or crash
- Empty cast shows "0" or appropriate message
- Multiple writer episodes display properly
- All date formats parse and sort correctly
- Special character titles render correctly

// Advanced tests (detect presence)
- Performance: Check for virtualization/pagination for large datasets
- Keyboard: Try pressing arrow/enter keys
- Smart sort: Check if search affects sort order
- Validation: Check console for warnings
```

### 5. Exam Instructions (`student-instructions.md`)

Create student-facing instructions with:

**Exam Details:**
- Duration: 2 hours
- Tools allowed: All online resources, LLMs, documentation
- Submission format: ZIP file with HTML/CSS/JS files
- File naming: `[student-id]-doctor-who-exam.zip`

**Getting Started:**
- Download starter template (optional, basic HTML structure)
- Download test data file
- Read specification carefully
- Test frequently with provided data

**Tips for Success:**
1. Start with basic functionality
2. Test with the provided data (contains edge cases)
3. Check browser console for errors
4. Verify all interactions work
5. Read any code you use/generate before submitting
6. Advanced features are optional - perfect basic functionality first

**Grading Philosophy:**
Explicitly state:
- Basic functionality (Tier 1): 60% - achievable with LLM help
- Edge case handling (Tier 2): +25% - requires testing and understanding
- Advanced features (Tier 3): +15% - requires problem-solving
- Working code with bugs: Partial credit
- Code that crashes: Point deductions
- Understanding demonstrated through working edge cases: Higher grades

**Submission Checklist:**
- [ ] All files in zip
- [ ] No external dependencies (CDNs ok)
- [ ] Works when opened locally
- [ ] Tested with provided data
- [ ] No console errors on load

### 6. Starter Template (`starter-template/`)

Generate a minimal starter template:

**Files:**
- `index.html` - Basic HTML5 structure with table placeholder
- `styles.css` - Minimal CSS reset and layout
- `script.js` - Empty with helpful comments indicating structure

**index.html should include:**
- Semantic HTML5 structure
- Table with appropriate headers
- Filter inputs
- Link to styles and script
- Comments indicating where to add functionality

**styles.css should include:**
- Basic reset
- Responsive table styling
- Sort indicator styles (arrow icons)
- Loading state styles
- Empty state for when no data matches filters

**script.js should include:**
```javascript
// Comment structure:
// 1. Configuration and constants
// 2. Data loading and parsing
// 3. Display functions
// 4. Sorting logic
// 5. Filtering logic
// 6. Event listeners
// 7. Initialization

// Helpful starter code:
const DATA_URL = 'doctor-who-episodes-exam.json';
let episodes = [];
let currentSort = { column: 'rank', ascending: true };

// TODO: Implement data loading
// TODO: Implement table rendering
// TODO: Implement sorting
// TODO: Implement filtering
```

### 7. Exam Variants (`variants/`)

Generate 5 exam variants (A-E) with:

**Common elements (same across all):**
- Tier 1 requirements (basic functionality)
- Same test data file
- Same point values

**Varying elements:**
- Different filter requirements in Tier 1
- Different edge cases emphasized in Tier 2
- Different advanced feature options in Tier 3

**Variant A:**
- Filters: Name, Era dropdown
- Edge cases focus: Null companions, date formats
- Advanced options: Performance, Keyboard nav, Smart sort, Validation

**Variant B:**
- Filters: Name, Writer dropdown
- Edge cases focus: Multiple writers, special characters
- Advanced options: Performance, Multi-column sort, Export CSV, Validation

**Variant C:**
- Filters: Name, Doctor dropdown
- Edge cases focus: Empty cast, mixed dates
- Advanced options: Keyboard nav, Smart sort, Decade grouping, Validation

**Variant D:**
- Filters: Name, Companion dropdown  
- Edge cases focus: Null companions, special characters
- Advanced options: Performance, Smart sort, Export CSV, Multi-column sort

**Variant E:**
- Filters: Name, Series number range
- Edge cases focus: All edge cases equally
- Advanced options: Keyboard nav, Validation, Decade grouping, Performance

## Technical Requirements

**Format:**
- Use modern JavaScript (ES6+)
- No framework requirements (vanilla JS acceptable)
- Should work in modern browsers (Chrome, Firefox, Safari latest)
- No build process required
- Can use CDN resources (no npm/install required)

**Code Quality Standards:**
- Clear variable names
- Comments explaining complex logic
- Consistent formatting
- No global namespace pollution
- Error handling with try-catch where appropriate

## Output Format

Generate all files in this structure:
```
exam-materials/
├── exam-specification.md
├── student-instructions.md
├── grading-rubric.md
├── doctor-who-episodes-exam.json
├── test-suite.html
└── starter-template/
    ├── index.html
    ├── styles.css
    └── script.js
```

## Additional Instructions

1. **Be specific but not prescriptive:** Describe what needs to be done, not how
2. **Include examples:** Show expected output for edge cases
3. **Be consistent:** Use same terminology throughout all documents
4. **Test data realism:** Make the Doctor Who data feel authentic
5. **Grading clarity:** Make rubric objective and measurable
6. **Variant fairness:** Ensure all variants are equal difficulty

## Tone and Style

- Professional but friendly
- Clear and unambiguous for requirements
- Encouraging in student materials
- Objective in grading materials
- Assume students have basic JavaScript knowledge
- Acknowledge LLM use as legitimate tool

## Success Criteria

Generated materials should:
✅ Allow LLM to generate basic solution (Tier 1)
✅ Require understanding for edge cases (Tier 2)  
✅ Require problem-solving for advanced features (Tier 3)
✅ Create natural variance in scores (not everyone 60% or 100%)
✅ Be fair and gradable with 70 students
✅ Teach proper LLM usage patterns
✅ Test practical web development skills

Generate all materials now.