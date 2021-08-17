# Angular Quickstart

This is an attempt to retrace Angular's evolution since v2.

As a starting point, I used Angular's [quickstart](https://web.archive.org/web/20161011223739mp_/https://angular.io/docs/ts/latest/quickstart.html), as of Oct 11, 2016.

## Fixing the quickstart

There were conflicts between `core-js` and `tsc`:

    > angular-quickstart@1.0.0 start /home/benoit/angular-quickstart
    > tsc && concurrently "tsc -w" "lite-server"

    node_modules/rxjs/Subject.d.ts:24:5 - error TS2416: Property 'lift' in type 'Subject<T>' is not assignable to the same property in base type 'Observable<T>'.
      Type '<T, R>(operator: Operator<T, R>) => Observable<T>' is not assignable to type '<R>(operator: Operator<T, R>) => Observable<R>'.
        Type 'Observable<T>' is not assignable to type 'Observable<R>'.
          Type 'T' is not assignable to type 'R'.

    24     lift<T, R>(operator: Operator<T, R>): Observable<T>;
          ~~~~


    node_modules/typescript/lib/lib.d.ts:105:14 - error TS2300: Duplicate identifier 'PropertyKey'.

    105 declare type PropertyKey = string | number | symbol;
                    ~~~~~~~~~~~


    typings/globals/core-js/index.d.ts:3:14 - error TS2300: Duplicate identifier 'PropertyKey'.

    3 declare type PropertyKey = string | number | symbol;

So I had to make a few changes in `package.json`. Use precise 2.4.1 version for `core-js`:

    -    "core-js": "^2.4.1",
    +    "core-js": "2.4.1",

And set typescript to 2.1.1 (support for spread operator):

    -    "typescript": "^2.0.3",
    -    "typings":"^1.4.0"
    +    "typescript": "^2.1.1",
    +    "typings": "^1.4.0"

Also, I removed the `start` script and used only `tsc:w`. In two separate shells:

* `npm run tsc:w`.
* `python3 -m http.server 8000`

