# My Linux Environment

## Introduce
> This is my linux environment, only need to pull repository and launch docker.
> If there's any change during developing, I will update this repository.

## Usage

1. clone repository
2. change username

> Username is setted to "leo" and don't have .env file at this stage. You can change all username to your username.


3. launch docker
```
docker-compose up -d
```

4. enter docker
```
docker exec -it linux bash
```

5. set new password
```
su $username
passwd
```

