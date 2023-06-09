# useSelection

## New Testament

```jsx
import React, { useEffect, useState } from 'react';

import { useSelection, tsvToJSON, verseObjectsToString } from '@texttree/tn-quote';
import { toJSON } from 'usfm-js';
import axios from 'axios';

function Component() {
  const [greek, setGreek] = useState();
  const [target, setTarget] = useState();
  const [tn, setTn] = useState();
  useEffect(() => {
    // 1TI
    const getData = async () => {
      const { data: greekRaw } = await axios.get(
        'https://git.door43.org/unfoldingWord/el-x-koine_ugnt/raw/branch/master/55-1TI.usfm'
      );
      const greek = toJSON(greekRaw).chapters;
      setGreek(greek);
      const { data: tnRaw } = await axios.get(
        'https://git.door43.org/ru_gl/ru_tn/raw/branch/master/tn_1TI.tsv'
      );
      const tn = tsvToJSON(tnRaw, ['Reference', 'Occurrence', 'Quote', 'Note'], true);
      setTn(tn);
      const { data: targetRaw } = await axios.get(
        'https://git.door43.org/ru_gl/ru_rlob/raw/branch/master/55-1TI.usfm'
      );
      const target = toJSON(targetRaw).chapters;
      setTarget(target);
    };
    getData();
  }, []);
  let data = 'loading';
  let selectedTn = '';
  if (greek && target && tn) {
    selectedTn = tn[11];
    data = useSelection({
      greekVerseObjects: greek[selectedTn.chapter][selectedTn.verse].verseObjects,
      targetVerseObjects: target[selectedTn.chapter][selectedTn.verse].verseObjects,
      quote: selectedTn.Quote,
      occurrence: selectedTn.Occurrence,
      chapter: 1,
      verses: [3],
    });
  }
  return (
    <>
      {selectedTn
        ? selectedTn.chapter + ':' + selectedTn.verse + ' ' + selectedTn.Quote
        : ''}{' '}
      - {data}
    </>
  );
}

<Component />;
```

## Old Testament

```js
import React, { useEffect, useState } from 'react';

import { useSelection, tsvToJSON } from '@texttree/tn-quote';
import { toJSON } from 'usfm-js';
import axios from 'axios';

function Component() {
  const [greek, setGreek] = useState();
  const [target, setTarget] = useState();
  const [tn, setTn] = useState();
  useEffect(() => {
    // RUT
    const getData = async () => {
      const { data: greekRaw } = await axios.get(
        'https://git.door43.org/unfoldingWord/hbo_uhb/raw/branch/master/08-RUT.usfm'
      );
      const greek = toJSON(greekRaw).chapters;
      setGreek(greek);
      const { data: tnRaw } = await axios.get(
        'https://git.door43.org/Es-419_gl/es-419_tn/raw/branch/master/tn_RUT.tsv'
      );
      const tn = tsvToJSON(tnRaw, ['Reference', 'Occurrence', 'Quote', 'Note'], true);
      setTn(tn);
      const { data: targetRaw } = await axios.get(
        'https://git.door43.org/Es-419_gl/es-419_glt/raw/branch/master/08-RUT.usfm'
      );
      const target = toJSON(targetRaw).chapters;
      setTarget(target);
    };
    getData();
  }, []);
  let data = 'loading';
  let selectedTn = '';
  if (greek && target && tn) {
    selectedTn = tn[29];
    data = useSelection({
      greekVerseObjects: greek[selectedTn.chapter][selectedTn.verse].verseObjects,
      targetVerseObjects: target[selectedTn.chapter][selectedTn.verse].verseObjects,
      quote: selectedTn.Quote,
      occurrence: selectedTn.Occurrence,
      chapter: 1,
      verses: [9],
    });
  }
  return (
    <>
      {selectedTn
        ? selectedTn.chapter + ':' + selectedTn.verse + ' ' + selectedTn.Quote
        : ''}{' '}
      - {data}
    </>
  );
}

<Component />;
```
