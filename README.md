# Flask Stripe PostgreSQL Bootstrapped
This template is ready for scaling and is easy to deploy.

![Signup, Login and Stripe Demo!](demo/showcase.gif)

# Technologies and features

- [x] Python & Flask & PostgreSQL Database
- [x] Stripe Subscriptions (Create, Cancel, Reactivate, Update supported)
- [x] Bootstrapped theme [Creative](https://startbootstrap.com/themes/creative/) and [SB Admin 2](https://startbootstrap.com/themes/sb-admin-2/)
- [x] Docker: Fully split into microservices. Runs with Docker Compose, but can **[easily be translated to Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes/)**
- [x] User sign up and login (Facebook & Google integration in progress)
- [x] 3 Pricing Tiers included (Starter, Growth, Scale)
- [x] Base templates: Index, Dashboard and Pages
- [x] Secure app: Protection against XSS, X-XSS, CSRF, clickjacking (iframe) attacks
- [x] Trial Period (defaults to 24 hours)
- [x] Notifications for users (upselling, credit card expiring soon, etc.)
- [ ] Feedback button: Easily gather feedback from users
- [ ] Email validation
- [ ] Multiprocessing with Gunicorn, for SQLAlchemy and MySQL
- [ ] Admin account: View feedback, logs, errors, etc.

## Future Work

1. Scaling the frontend.

Check out Martin Fowler's website with this [great article](https://martinfowler.com/articles/micro-frontends.html) by Cam Jackson on splitting your frontend into microservices. Probably not necessary for most (99%), but consider it.

2. Scaling the databases

Start separating into databases instead of tables; right now, there exists one table for each service. You should definitely think about scaling the database, a cloud option is a great option here.

3. Less coupling

Currently, the different services knows about eachother (which means higher coupling). To remove this, we would want a centralized service that knows all the services, but the rest of the services don't know about eachother. All communication would go through this centralized service.

Most of the work is done, and it would just be changing some endpoints, but if you want truly low coupling, this needs a migration.

## System Overview

This is a simple overview of the system. Go to the app folder and see the technical README for a more detailed overview.

![System Overview](demo/simple-system-overview.png)

## Todo

- Move on to upgrading/downgrading monthly and yearly plans
- Add billing information (invoice date, description, amount, was it paid)
- Variable builder

# How To Run The Application (After Installation)

You should make sure that your database is running first and foremost, else the following will fail. Look under installation for Windows or Mac/Linux for how to run the database locally. It just needs to be running in the background, all the databases and tables are created programmatically.

1. Simply navigate (in a terminal) into the ~/app folder.
2. Run `docker-compose build` for your first build and when you have made changes.
3. Run `docker-compose up` to run all the services.

Please configure `~/app/setup_app/config.py` as needed. I recommend making a mode for development and production (staging if necessary) with all the needed credentials. The file is very easy to extend with new config secrets.

Note that scaling is very easy, you can just convert your `docker-compose.yml` file to Kubernetes files, and you can easily get set up and running in Google Cloud Platform or Amazon Web Services. [Read this tutorial for more](https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes/).

## Receiving webhooks from Stripe

For payments, Stripe needs to be able to send you webhooks. You can enable Stripe's test mode to make sure your setup is correct. I have used [ngrok](https://ngrok.com/) (free) to do this. It's really simple, you just navigate to the folder and run `./ngrok http 5004` or whichever port the Stripe service is running on.

Other choices are:

https://localtunnel.github.io/www/

http://localhost.run/

# Installation (Development)

1. Install Python (3.7 was used for this project)
2. Install the package requirements `pip install -r requirements.txt`
3. Download and install PostgreSQL server and run it
4. Configure your connector in `app/setup_app/config.py`. I configured PostgreSQL to run on port 5432, but the default port is 3306, which you can easily switch the port to in the code.
5. Install Docker

### Login to PostgreSQL database from Mac and Linux

Type in `psql postgres` and press enter. It will ask for your password, then you are in.
