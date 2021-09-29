## Image Size 

Reduce size of the image

```
RUN apt-get clean && rm -f /var/lib/apt/lists/*_*
```

Combine update, install and clean:

```
RUN apt-get update -y \
&& apt-get install -y -q package-name \
&& apt-get clean \
&& rm -f /var/lib/apt/lists/*_*
```

## Build Stage

Use a separate build stage

```
FROM base-image AS builder
COPY . /app

RUN apt-get install build-essential \
&& bundle install --deployment

FROM base-image
COPY --from=builder /app /app
```

## System Locale

Set the system locale

```
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
&& locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
```

## User

Create an unprivileged user.

# After build

```
RUN adduser -s /bin/sh -u 1001 -G root \
-h /app -S -D rails \
&& chown -R rails /app

USER rails
```

Prefer exec form for CMD

```
CMD ["bundle", "exec", "rails", "s"]
```

Specify resource constraints in production requests:

```
  memory: "100Mi"
  cpu: 0.5
 limits:
  memory: "200Mi"
  cpu: 1.0
```

Log to STDOUT or an external agent

```
ENV RAILS_LOG_STDOUT=true
```

