```ts

export type Result<T, E> =
  | {
      ok: true;
      value: T;
    }
  | {
      ok: false;
      value: E;
    };

export const ok = <T>(value: T): Result<T, never> => ({
  ok: true,
  value,
});

export const fail = <T>(value: T): Result<never, T> => ({
  ok: false,
  value,
});

type Response = {
  username: string;
  email: string;
};

type ResponseError = {
  value: { error: true };
  error: string;
};

function main(value: boolean): Result<Response, ResponseError> {
  if (!value) {
    return fail({
      error: "error",
      value: {
        error: true,
      },
    });
  }

  return ok({
    email: "email",
    username: "username",
  });
}

const response = main(true);

if (!response.ok) {
  const { error, value } = response.value;

  console.log({
    error,
    value,
  });
} else {
  const { username, email } = response.value;

  console.log({
    username,
    email,
  });
}

```
