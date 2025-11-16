# EduVault - E-Learning Platform

## Overview
A comprehensive Django-based e-learning platform with role-based access control (Admin, Tutor, Student), course management, quiz system, and Stripe payment integration.

## Project Status
- **Database**: ✅ Fully configured and migrated
- **Backend**: ✅ Complete implementation
- **URL Routing**: ✅ All routes configured
- **Templates**: ⚠️ Partial (dashboards done, others need creation)
- **Payment Integration**: ✅ Stripe configured (needs API keys)

## Recent Changes (Nov 9, 2025)
### Database & Setup
- Created PostgreSQL database with all migrations applied
- Created media and static directories for file uploads
- Generated admin superuser (username: admin, password: admin123)

### Backend Implementation
**Admin Functionality:**
- User management (create/edit/delete users, create tutors)
- Course management (CRUD operations)
- Platform analytics dashboard
- Tutor-course assignment

**Tutor Functionality:**
- Manage own courses
- Create course units/modules
- Upload materials (PDFs, slides, videos)
- Create quizzes with questions and auto-grading
- View student progress and analytics
- Track student attendance (automatic via video watch time)

**Student Functionality:**
- Browse course catalog
- View course details
- Enroll in courses (free or paid)
- Access learning dashboard with enrolled courses
- Watch videos with progress tracking
- Take quizzes with immediate feedback
- View quiz results and scores

**Payment System:**
- Stripe checkout integration
- Payment intent creation
- Webhook handling for payment confirmation
- Automatic course enrollment on successful payment

### Templates Completed
- ✅ Enhanced admin dashboard
- ✅ Enhanced tutor dashboard
- ✅ Enhanced student dashboard
- ✅ Admin user management pages
- ✅ Base template with navigation
- ✅ Login/Register pages
- ✅ Home page

### Templates Still Needed
The following templates need to be created (Django will show TemplateDoesNotExist errors until these are added):

**Course Management (Admin/Tutor):**
- `templates/courses/admin_manage_courses.html`
- `templates/courses/admin_create_course.html`
- `templates/courses/admin_edit_course.html`
- `templates/courses/tutor_my_courses.html`
- `templates/courses/tutor_course_detail.html`
- `templates/courses/tutor_create_unit.html`
- `templates/courses/tutor_edit_unit.html`
- `templates/courses/tutor_add_video.html`
- `templates/courses/tutor_add_material.html`
- `templates/courses/tutor_student_progress.html`

**Student Course Views:**
- `templates/courses/catalog.html`
- `templates/courses/course_detail.html`
- `templates/courses/my_courses.html`
- `templates/courses/course_learn.html`

**Payment Templates:**
- `templates/payments/checkout.html`
- `templates/payments/success.html`
- `templates/payments/history.html`

**Quiz Templates:**
- `templates/quizzes/tutor_create_quiz.html`
- `templates/quizzes/tutor_edit_quiz.html`
- `templates/quizzes/tutor_add_question.html`
- `templates/quizzes/tutor_quiz_analytics.html`
- `templates/quizzes/take_quiz.html`
- `templates/quizzes/results.html`

## User Roles & Capabilities

### Admin
- Login: `/admin-dashboard/`
- Create tutors: `/admin/users/create-tutor/`
- Manage all users: `/admin/users/`
- Create/edit/delete courses: `/admin/courses/`
- Assign tutors to courses
- View platform analytics (users, courses, revenue)

### Tutor  
- Login: `/tutor-dashboard/`
- View my courses: `/tutor/courses/`
- Create course units with videos and materials
- Create quizzes for videos: `/tutor/quizzes/create/{video_id}/`
- View student progress: `/tutor/courses/{id}/progress/`
- View quiz analytics
- Auto attendance tracking based on video watch time

### Student
- Login: `/student-dashboard/`
- Browse courses: `/courses/`
- View course details: `/courses/{slug}/`
- Enroll (free or paid): `/courses/{id}/checkout/`
- Access learning materials: `/courses/{id}/learn/`
- Take quizzes: `/quizzes/{id}/take/`
- View results: `/quizzes/attempts/{id}/results/`
- Track progress automatically

## Quick Start

### Access the Platform
1. **Homepage**: http://localhost:5000/ (or your Replit URL)
2. **Admin Login**: 
   - Username: `admin`
   - Password: `admin123`
   - Go to: http://localhost:5000/admin-dashboard/

### First Steps as Admin
1. Login as admin
2. Create categories via Django admin: http://localhost:5000/admin/ → Categories
3. Create a tutor: `/admin/users/create-tutor/`
4. Create a course: `/admin/courses/create/` (assign to tutor)

### As Tutor (after creation by admin)
1. Login with tutor credentials
2. View your courses: `/tutor/courses/`
3. Add units to courses
4. Upload videos and materials
5. Create quizzes for videos

### As Student (register yourself)
1. Register: `/accounts/register/` (select Student role)
2. Browse courses: `/courses/`
3. Enroll in free courses or purchase paid ones
4. Start learning: `/courses/{id}/learn/`

## Configuration

### Stripe Payment Setup
To enable payments, add these environment variables:
```bash
STRIPE_PUBLIC_KEY=pk_test_...
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...
```

### Database
Already configured with PostgreSQL using Replit's built-in database. Connection details are in environment variables.

### Media Files
Media files (videos, PDFs, images) are stored in:
- `media/profiles/` - User profile pictures
- `media/course_thumbnails/` - Course images
- `media/videos/` - Uploaded videos
- `media/video_thumbnails/` - Video thumbnails
- `media/materials/` - Course materials (PDFs, slides)

## Technical Architecture

### Models
- **User**: Custom user model with roles (admin, tutor, student)
- **Course**: Courses with tutors, categories, pricing
- **Unit**: Course modules/chapters
- **Video**: Video lessons with progress tracking
- **Material**: Downloadable course materials
- **Quiz**: Quizzes attached to videos
- **Question/Answer**: Quiz questions with auto-grading
- **Purchase**: Payment and enrollment records
- **VideoWatch**: Track student video progress
- **Attendance**: Auto attendance based on watch time

### Key Features
- **Role-based permissions**: Decorator-based access control
- **Auto-grading**: Quizzes automatically calculate scores
- **Progress tracking**: Video watch progress, course completion
- **Attendance**: Automatic based on video engagement
- **Payment integration**: Stripe checkout and webhooks
- **Media uploads**: Support for videos, PDFs, images

## Next Steps
1. Create remaining templates (see list above)
2. Configure Stripe API keys for payment testing
3. Add sample data (categories, courses)
4. Test all three user role workflows
5. Customize templates with branding/styling
6. Add email notifications (optional)
7. Implement certificate generation (optional)

## Known Issues
- Templates for most views need to be created (backend complete)
- Tailwind CSS via CDN (should use PostCSS for production)
- No email verification implemented yet
- File size limits not configured

## Technology Stack
- **Backend**: Django 5.2.7
- **Database**: PostgreSQL (Neon)
- **Frontend**: Tailwind CSS
- **Payment**: Stripe
- **File Storage**: Local filesystem (media folder)
- **Authentication**: Django built-in auth with custom User model

## User Preferences
- None specified yet

## Development Notes
- All migrations applied successfully  
- Server running on port 5000
- Debug mode enabled (disable for production)
- CSRF trusted origins configured for Replit domains
