```
import { Injectable } from '@nestjs/common';
import * as fs from 'fs-extra';
import * as path from 'path';

@Injectable()
export class FileService {
  private readonly filePath = path.resolve(__dirname, 'data.json');

  async writeToFile(data: Record<string, any>): Promise<void> {
    try {
      await fs.writeJson(this.filePath, data, { spaces: 2 });
    } catch (err) {
      throw new Error(`Error writing to file: ${err.message}`);
    }
  }

  async readFromFile(): Promise<Record<string, any>> {
    try {
      const data = await fs.readJson(this.filePath);
      return data; // data will be a JavaScript object
    } catch (err) {
      if (err.code === 'ENOENT') {
        // File doesn't exist, return an empty object
        return {};
      }
      throw new Error(`Error reading from file: ${err.message}`);
    }
  }

  async clearFile(): Promise<void> {
    try {
      // Write an empty object to the file
      await fs.writeJson(this.filePath, {});
    } catch (err) {
      throw new Error(`Error clearing file: ${err.message}`);
    }
  }
}


```
